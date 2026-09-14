<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/enablertp-returns-waapi-error-access-denied-for-avira-security -->

# EnableRTP returns WAAPI_ERROR_ACCESS_DENIED for Avira Security

## [**1. Symptom**](/docs/mdsdk/knowledge-base/enablertp-returns-waapi-error-access-denied-for-avira-security#1-symptom)

An integration calls `EnableRTP` (method 1005) against **Avira Security** on Windows, and the call fails with `WAAPI_ERROR_ACCESS_DENIED` (-22). Running the integrating application with administrator privileges — or even as `NT AUTHORITY\SYSTEM` — does not change the result. Real-time protection stays off.

### [**Applies to**](/docs/mdsdk/knowledge-base/enablertp-returns-waapi-error-access-denied-for-avira-security#applies-to)

| OESIS method | `EnableRTP` (method ID 1005) |
| --- | --- |
| Platform | Windows |
| Third-party product | Avira Security (Signature ID: `3636`) |
| Product version verified | 1.1.115.3317 |
| OESIS SDK version verified | 4.3.6110 |
| Returned error code | `WAAPI_ERROR_ACCESS_DENIED` (`-22`) |

The behavior is confirmed on the Avira version above. It has **not** been version-ranged across the Avira product line — earlier Avira builds used with earlier OESIS versions were reported as working by the reporting customer.

## [**2. Cause**](/docs/mdsdk/knowledge-base/enablertp-returns-waapi-error-access-denied-for-avira-security#2-cause)

To enable real-time protection, OESIS does not manipulate Avira's settings directly. It asks **Avira's own management interface** to perform the operation and reports the vendor's result back to the caller. For this method OESIS:

- does **not** evaluate permissions,
- does **not** inspect the caller's access token, and
- does **not** deny the operation itself — there is no such logic on the OPSWAT side for `EnableRTP`.

In OPSWAT's reproduction the evidence was unambiguous: **the OESIS engine completed its part successfully.** The operation was rejected by Avira: the product's own component exited with a non-zero status and returned an explicit *access denied* response. The SDK surfaced that vendor refusal to the caller as `WAAPI_ERROR_ACCESS_DENIED` (`-22`). In other words, error code `-22` the caller receives is **Avira's answer passed through**, not a decision made by OESIS.

### [***Why elevating privileges does not help***](/docs/mdsdk/knowledge-base/enablertp-returns-waapi-error-access-denied-for-avira-security#why-elevating-privileges-does-not-help)

Avira applies its own internal validation before accepting a request to change a protection setting. That logic is neither visible nor documented to OPSWAT — we can observe its verdict, but not its criteria.

What can be stated with certainty is that **privilege level is not the deciding factor**: Avira refused the request while the SDK held the full `NT AUTHORITY\SYSTEM` privilege set, the highest available on the machine. Escalating privileges further is therefore not a viable workaround — something else about the calling environment is being evaluated, and only Avira can say what.

## [**3. Resolution / workaround**](/docs/mdsdk/knowledge-base/enablertp-returns-waapi-error-access-denied-for-avira-security#3-resolution--workaround)

On the same machine, with the same privileges and the same Avira build, the result differed by **how the SDK was hosted**:

| SDK hosting model | `EnableRTP` result |
| --- | --- |
| Spawned as a normal process by a parent process (for example a test framework or PsExec) — even running as `SYSTEM` | FAILS — returns `-22` |
| Hosted as a genuine Windows service, started by the Service Control Manager | SUCCEEDS |

### [***Why "hosted as a service" is not the same as "running as SYSTEM"***](/docs/mdsdk/knowledge-base/enablertp-returns-waapi-error-access-denied-for-avira-security#why-hosted-as-a-service-is-not-the-same-as-running-as-system)

Both processes can hold the same `NT AUTHORITY\SYSTEM` identity, yet they are not equivalent:

| Aspect | Spawned as a normal process | Hosted as a real Windows service |
| --- | --- | --- |
| Started by | A parent process — the integrating application, a test framework, PsExec | The Windows Service Control Manager |
| Token origin | Inherited or duplicated from the parent process | Created by the operating system for the service |
| Service identity in the token | Absent | Carries the `NT AUTHORITY\SERVICE` group, and a per-service SID (`NT SERVICE\<name>`) when the service is configured with one |
| Windows session | Depends on how the parent was launched | Always session 0, service window station |
| Process image and parent chain seen by security software | A child process of the integrating application | A service image started by the SCM |

OPSWAT is **NOT** claiming which of these Avira evaluates. Security products commonly validate the identity, registration, or parent chain of whatever asks them to change a protection setting, not merely its privileges — but that logic is internal to Avira, and only Avira can confirm the actual requirement.

### [**What to do**](/docs/mdsdk/knowledge-base/enablertp-returns-waapi-error-access-denied-for-avira-security#what-to-do)

1. **If your integration can host the SDK as a genuine Windows service, do that.** This is the configuration OPSWAT observed working for this Avira version. Note that a process merely *running as* `SYSTEM` is not sufficient — see the comparison above.
2. **If hosting the SDK as a service is not viable for your deployment**, treat `EnableRTP` as **not supported** for the affected Avira versions, and handle -22 from this method as an expected, non-recoverable outcome rather than retrying with higher privileges.
3. **To pursue the operation in a non-service deployment**, raise the exact prerequisites with Avira directly, since the accept/deny decision is made entirely inside their product.

The service-hosting result is an **empirical lab observation**, not a supported or guaranteed configuration. OPSWAT has not identified Avira's exact requirement and does not claim to.

## [**4. What still works**](/docs/mdsdk/knowledge-base/enablertp-returns-waapi-error-access-denied-for-avira-security#4-what-still-works)

Only the *enable* action is refused. Detecting Avira Security and reporting its real-time protection state continue to work normally: an integration can still determine whether real-time protection is on or off through `GetRealTimeProtectionState` and surface that to the end user or policy engine, even where it cannot turn it on.

## [**5. FAQ**](/docs/mdsdk/knowledge-base/enablertp-returns-waapi-error-access-denied-for-avira-security#5-faq)

**Will a future OESIS SDK release fix this?**
No. The refusal originates inside Avira, so there is nothing on the OESIS side that can grant an operation the vendor declines. Returning a different error code would only hide the vendor's answer without making the operation succeed.

**Is this a permissions bug in the SDK?**
No. OESIS performs no permission check for this method, and the refusal occurred while the SDK held the highest privilege set available on the machine.

**We already run the SDK as** `NT AUTHORITY\SYSTEM` **— why is that not enough?**
Because "running as SYSTEM" and "being a Windows service" are different things. A process started by another process inherits its token and carries no service identity, while a service is started by the Service Control Manager with a token the OS builds for it. See [Why elevating privileges does not help](/docs/mdsdk/knowledge-base/enablertp-returns-waapi-error-access-denied-for-avira-security#why-elevating-privileges-does-not-help).

**Does it affect other Avira versions?**
Only Avira Security 1.1.115.3317 has been verified. Other builds have not been swept, and a future Avira build could behave differently in either direction.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

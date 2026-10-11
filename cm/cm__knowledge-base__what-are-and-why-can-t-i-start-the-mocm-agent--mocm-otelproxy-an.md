<!-- source: https://www.opswat.com/docs/cm/knowledge-base/what-are-and-why-can-t-i-start-the-mocm-agent--mocm-otelproxy-an -->

# What are and why can't I start the mocm-agent, mocm-otelproxy and mocm-otelcol-gate services on My OPSWAT Central Management on Linux?

> **Check Your Version:**
>
> This article applies to My OPSWAT Central Management 10.7.26080 and later, deployed on-premises on Linux systems (RPM or OVA). It does not apply to Windows deployments.

## **Overview**

After installing or upgrading My OPSWAT Central Management on-premises on Linux (RPM or OVA), administrators may notice three systemd units that are not running:

- `mocm-agent.service`
- `mocm-otelproxy.service`
- `mocm-otelcol-gate.service`

Attempting to start them manually appears to do nothing. The command returns without an error, and the unit remains inactive.

**In this situation no action is required.** These units are not part of the core Central Management application, and Central Management is fully operational without them.

## **Why these services do not start**

The three units belong to an optional infrastructure telemetry component that is included with the Linux packages from version 10.7.26080 onward.

| Unit | Role |
| ---- | ---- |
| `mocm-agent.service` | Collects host and service health metrics from the appliance |
| `mocm-otelproxy.service` | Local relay that forwards those metrics outbound |
| `mocm-otelcol-gate.service` | Timer-driven unit that checks whether telemetry has been enabled |

Telemetry collection is **disabled by default** on every new installation and upgrade. It is enabled only if an administrator deliberately turns it on.

While telemetry is disabled, `mocm-agent` and `mocm-otelproxy` carry a systemd start condition that is not satisfied. When you run `systemctl start` against them, systemd evaluates that condition, skips the unit, and reports the command as successful. This is why the command appears to do nothing and why no error is written to the journal — the units are behaving exactly as designed.

The three units are attached to `mocm-infra.target` and `mocm-all.target` as optional dependencies only. They can never prevent Central Management from starting or running.

## **Confirming your deployment is healthy**

Run the following to verify the overall state of the product:

```powershell
sudo systemctl status mocm-all.target
sudo systemctl --failed
```

Expected results on a healthy system with telemetry disabled:

- `mocm-all.target` is **active**
- `mocm-agent.service` and `mocm-otelproxy.service` are **inactive (dead)**
- `mocm-otelcol-gate.timer` is **active (waiting)** — this is the normal state for the timer; it wakes periodically, checks the telemetry setting, and exits
- `systemctl --failed` lists no MOCM units

If that is what you see, the deployment is healthy and the three inactive units require no attention.

## **When it is an actual failure**

The behaviour above applies only when the units are **inactive**. If any MOCM unit reports **failed**, or exits with a non-zero status, that is a different problem and is not explained by this article.

In that case, restart the service stack:

```powershell
sudo systemctl restart mocm-all.target
```

If units remain in a failed state after the restart, generate a support package and open a case with OPSWAT Support:

[How to generate a support package for My OPSWAT Central Management? - My OPSWAT Central Management](https://www.opswat.com/docs/cm/knowledge-base/how-to-generate-a-support-package-for-my-opswat-central-manageme)

## **Notes**

- The telemetry units communicate only over loopback addresses. They do not open any externally reachable listener on the host.
- Do not manually create or edit the telemetry state file at `/etc/opt/mocm/optel-enabled`. It is managed by the product, and editing it by hand can leave the telemetry components in an inconsistent state.
- Uninstalling Central Management removes the stored telemetry setting, so a later reinstall will not silently re-enable telemetry.

> If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)

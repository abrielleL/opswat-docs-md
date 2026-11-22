<!-- source: https://www.opswat.com/docs/mdcluster/operating/operating-security -->

# Security

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This section will allow the system administrator to enable secure connections to MetaDefender Cluster Control Center if required. In addition, Request rate limit, Password and Session policies are set in this section. These settings are found under **Settings** > **Security** tab.

### [Request Rate Limit](/docs/mdcluster/operating/operating-security#request-rate-limit)

The **Request Rate Limit** feature helps protect MD Cluster Control Center from excessive administrative requests by limiting the number of concurrent operations the system accepts. This prevents bursts of requests from overwhelming system resources and helps maintain stable performance.

Click **Details** to configure request rate limits for supported administrative operations. Each operation can be enabled or disabled independently, and its maximum number of concurrent requests can be adjusted to match your deployment requirements.

After you save the configuration, the new request rate limits may take up to **30 seconds** to take effect.

#### [Add Worker](/docs/mdcluster/operating/operating-security#add-worker)

Limits the number of **Add Worker** operations that can run concurrently.

When enabled, specify the maximum number of Worker registration requests that MD Cluster Control Center can process at the same time. Requests that exceed the configured limit are rejected, and users are prompted to try again later.

The updated limit may take up to **30 seconds** to take effect after it is saved.

---

### [Password Policies](/docs/mdcluster/operating/operating-security#password-policies)

Info

These password policies changes only apply to new user creations and future password changes. Existing users' passwords are unaffected.

Local users' password can be enforced to meet requirements set by administrators, which includes following constraints:

- **Enforce Password History** (**Passwords Remembered (0-24)**):

  - Determines the number of unique new passwords that must be associated with a user account before an old password can be reused.
  - Range: [0-24].
  - Default: 0 (to disable enforcement).
- **Password Must Meet Complexity Requirements:**

  - Determines whether passwords must meet a series of guidelines that are considered important for a strong password.
  - Default: Disabled

Complexity requirements

- At least 4 characters in length.
- At least 1 uppercase letter of European languages (A through Z).
- At least 1 lowercase letter of European languages (a through z).
- At least 1 base 10 digits (0 through 9).
- At least 1 non-alphanumeric characters (special characters): (~!@#$%^&*_-+=`|(){}[]:;"'<>,.?/).

- **Enforce Min Password Length** (**Min Password Length (0-30)**):

  - The least number of characters that can make up a password for a user account.
  - Range: [0-30].
  - Default: 0 (to disable enforcement).

---

### [Session Policies](/docs/mdcluster/operating/operating-security#session-policies)

**Session policies** control how user sessions are created and maintained in MD Cluster. You can configure session expiration, allow or prevent multiple concurrent sessions for the same user, and control whether requests from different IP addresses are accepted within an authenticated session.

Changes take effect for new sessions. Existing sessions continue to use the settings that were in effect when they were established.

- **Enable Idle Session Timeout** / **Idle Session Timeout**: Idle timeout to invalidate individual user’s session based on that user last activity.
- **Enable Session Timeout** / **Session Timeout**: Absolute timeout to invalidate individual user’s session regardless of that user activities.
- **Allow Duplicate Sessions**: Allow same user to have multiple active sessions.
- **Allow Cross IP Sessions**: Allow requests coming from sources different from the authenticated origin.

### [Scan From Link](/docs/mdcluster/operating/operating-security#scan-from-link)

These settings control how MetaDefender Cluster downloads files that are submitted by link (the `downloadfrom` header of `POST /file`). They apply to the whole cluster.

- **Max Download Queue**: the number of downloads that can run at the same time.

  - When the limit is reached, a new link is **not** refused. It waits in the queue and starts when a running download finishes.
  - Use a lower value to limit the network and disk load on the Download Service. Use a higher value to download more files in parallel.
- **Idle Timeout**: How long a download can go without receiving any data before it stops.

  - The value is in **milliseconds**.
  - The timer restarts every time data arrives. A slow download that still receives data does not stop.
  - When the timeout is reached, the download result is `Download Failed` with the error detail `Server took too long to respond`.

The idle timeout does not limit the total download time.

- **Enforce Scan From Link Validation**: Turn this on to allow or block links by pattern. When it is off, every link is downloaded, and the **Validation Type** and **Patterns** are ignored.

| **Validation Type** | A link is downloaded when |
| --- | --- |
| Blocklist | It matches none of the patterns. |
| Allowlist | It matches at least one pattern. |

- **Patterns**: Each pattern is a regular expression.

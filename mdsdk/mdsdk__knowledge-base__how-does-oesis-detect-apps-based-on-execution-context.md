<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-does-oesis-detect-apps-based-on-execution-context -->

# How Does OESIS SDK Detect Applications Based on Execution Context?

### [Overview](/docs/mdsdk/knowledge-base/how-does-oesis-detect-apps-based-on-execution-context#overview)

This article explains how the OESIS SDK detects installed applications depending on the **execution context** under which it runs. Understanding this behavior is essential for correctly configuring your deployment and ensuring comprehensive application visibility across all users on an endpoint.

The SDK supports two execution contexts:

- **SYSTEM Context** — typically used when the SDK runs as a Windows service.
- **USER Context** — used when the SDK runs as a user-level process.

### [Application Installation Types](/docs/mdsdk/knowledge-base/how-does-oesis-detect-apps-based-on-execution-context#application-installation-types)

Before reviewing detection behavior, it is important to understand the two types of application installations:

- **Per-Machine Applications** — Installed for all users on the system. Configuration and data are stored in system-wide directories (e.g., *Program Files*), accessible by any execution context.
- **Per-User Applications** — Installed for a specific user only. Configuration and data are stored in user-specific directories (e.g., , ), which are only accessible when that user's session is active.

### [Detection Behavior](/docs/mdsdk/knowledge-base/how-does-oesis-detect-apps-based-on-execution-context#detection-behavior)

#### [System Context](/docs/mdsdk/knowledge-base/how-does-oesis-detect-apps-based-on-execution-context#system-context)

When the OESIS SDK runs under **SYSTEM context** (e.g., as a Windows service), the following detection behavior applies:

**What is Detected**

- **Per-Machine Applications** — Always detected. These apps are installed in system-wide directories accessible from the SYSTEM context.
- **Per-User Applications (Current Active User)** — Detected when a user is actively logged in. The SDK can access the active user's application data through the current user session.

**What is NOT Detected**

- **Per-User Applications installed by another user** — Not detected, as the SDK does not have access to other users' session data.
- **Per-User Applications when no user is active** — Not detected, as there is no active user session to reference.

#### [User Context](/docs/mdsdk/knowledge-base/how-does-oesis-detect-apps-based-on-execution-context#user-context)

When the OESIS SDK runs under **USER context** (e.g., as a user-level process), the following detection behavior applies:

**What is Detected**

- **Per-Machine Applications** — Always detected. System-wide directories are accessible regardless of the execution context.
- **Per-User Applications (Current User)** — Detected. The SDK runs within the user's own session and has direct access to that user's application data.

**What is NOT Detected**

- **Per-User Applications installed by another user** — Not detected. A user-level process does not have access to other users' session directories.

### [Behavior Matrix](/docs/mdsdk/knowledge-base/how-does-oesis-detect-apps-based-on-execution-context#behavior-matrix)

| Execution Context | Scenario | Per-machine Apps | Per-user Apps (Current User) | Per-user Apps (Another Users) |
| --- | --- | --- | --- | --- |
| **Service** **(SYSTEM Context)** | Active User | Detected | Detected | Not Detected |
| **Service** **(SYSTEM Context)** | No Active User | Detected | Not Detected | Not Detected |
| **User-Level Process** **(USER Context)** | Active User | Detected | Detected | Not Detected |

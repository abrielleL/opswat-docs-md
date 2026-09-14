<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/difference-between-getagentstate-and-getrunningstate-of-wua -->

# Difference between GetAgentState and GetRunningState when using WUA

This article is applied to MetaDefender Endpoint Security SDK releases deployed on Windows.

## [**Overview**](/docs/mdsdk/knowledge-base/difference-between-getagentstate-and-getrunningstate-of-wua#overview)

When working with Windows Update Agent (WUA), MetaDefender Endpoint Security SDK offer two key methods: `GetAgentState` and `GetRunningState` to inspect the WUA agent status. This article will explains how each method works and what output is expected from it.

---

## [**Understanding GetAgentState Method**](/docs/mdsdk/knowledge-base/difference-between-getagentstate-and-getrunningstate-of-wua#understanding-getagentstate-method)

The `GetAgentState` method checks if the Windows Update Agent **is enabled**. This means it looks at whether the service **is allowed to run**, based on its system configuration. It **does not** tell you if the service is currently running — that will be handled by `GetRunningState`.

### [How it works](/docs/mdsdk/knowledge-base/difference-between-getagentstate-and-getrunningstate-of-wua#how-it-works)

- If Windows Update service (**wuauserv**) **is running**: → `enabled: true`
- If the service **is** **not running**, then it looks at the startup settings:

  - If the startup type is **Manual** or **Automatic**: → `enabled: true` (The system allows it to run if needed)
  - If the startup type is **Disabled**: → `enabled: false` (The system is set to never allow it to start)

To summarize, `GetAgentState` can return `enabled: true` result even if the update agent not currently running — as long as it isn’t disabled in the system settings.

## [**Understanding GetRunningState method**](/docs/mdsdk/knowledge-base/difference-between-getagentstate-and-getrunningstate-of-wua#understanding-getrunningstate-method)

While `GetAgentState` tells you whether the update agent is **enabled**, `GetRunningState` method reports whether the Windows Update Agent (**wuauserv**) service is **actively running at the moment**.

Info

Use this when you want real-time insight into the service's operational state, rather than its ability to be started.

### [How it works](/docs/mdsdk/knowledge-base/difference-between-getagentstate-and-getrunningstate-of-wua#how-it-works)

- If the **Windows Update service is running**: → `running: true`
- If the service is **not running**: → `running: false`

Unlike `GetAgentState`, this method will **not** consider about the startup settings or whether the service is enabled. `GetRunningState` simply reports the current status of the service.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

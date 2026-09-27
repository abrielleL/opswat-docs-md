<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-do-i-turn-on-off-the-compliance-check-function-in-the-my-ops -->

# How do I turn on/off the compliance check function in the OPSWAT Central Management console?

> **Check Your Product:**
>
> This article applies to OCM V7.5+ and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

OPSWAT Central Management’s optional **Perform compliance check** setting allows administrators to **Enable**/**Disable** MetaDefender Endpoint’s compliance check function on all managed devices.

To access this setting, please follow the instructions below.

1. Log into the **OPSWAT Central Management Console**, then navigate to **Settings>Global Settings>Device Agents**.
2. Under the **Compliance Report** section, check (**Enable**) or uncheck (**Disable**) the option to **Perform compliance check**, as needed, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/9jd0/iedpkvedb6ltlt3125iotydxkdwpqg9p0hcos8uj3e9byxo62yu7029ofuz7menj.png)

3. Scheduling options (where **X** is an adjustable time interval) include:

- **Agents will perform a compliance check every X minutes**
- **Agents will scan missing patches every X minutes**
- **Agents will run a custom script every X minutes**
- **Agent starts collecting compliance data in X minutes after the agent starts with the operating system.**

4. Once all is configured to your preference, implement your settings by the clicking **Save** button in the upper right-hand corner of the screen.

> **Please Note:**
>
> Should you choose to **Disable** the **Perform compliance check** option, please note that, along with the disabling of scheduled, automatic checks, the ability to manually trigger a compliance check will also be disabled. This trigger is usually accessible by navigating to the **OPSWAT Central Management Console>Inventory>Devices**, checking the boxes alongside the relevant devices, then clicking on the **ACTIONS** drop-down menu in the upper right-hand corner of the list and selecting **Compliance Check**, as illustrated below.
>
> ![](https://uploads.developerhub.io/prod/2x2P/pd8f8owt6p47fixanf0dq44pj4braub3ik3latwtm3yhlf642asm0bbi83dnww50.png)

> **Support:**
>
> If you have further queries, concerns or issues regarding **Configuring The** **MetaDefender Endpoint** **Compliance Check Function Via The OPSWAT Central Management Console**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)

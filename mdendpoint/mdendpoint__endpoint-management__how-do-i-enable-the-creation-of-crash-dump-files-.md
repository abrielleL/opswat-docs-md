<!-- source: https://www.opswat.com/docs/mdendpoint/endpoint-management/how-do-i-enable-the-creation-of-crash-dump-files- -->

# How do I enable the creation of Crash Dump files?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases subsequent to Version 7.6.x.x deployed on Windows systems.

> **Please Note:**
>
> Starting with MetaDefender Endpoint version Should be 7.6.x.x for Windows, program crash dump generation by default is disabled.
>
> This change is intended to preserve disk space, as most crashes are recoverable, so crash dump analysis will not be necessary.

In rare circumstances however, customers may choose to enable crash dump generation for detailed troubleshooting.

To assist, OPSWAT has released a utility that allows users to turn crash dump generation on and off again when required.

To enable/disable crash dump generation, please follow the instructions below.

1. Download the necessary **tool** from the relevant link below:

- For persistent Windows Client: [changeCrashDump.exe](https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/changeCrashDump.exe)
- For on-demand Windows Client: [changeCrashDump_OD.exe](https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/changeCrashDump_OD.exe)

2. Open a **Command Prompt** and select the **Run As Administrator** option.
3. Execute the command **change crashDump.exe <option>** choosing the relevant value from the options below:

- **ON**: to *enable* crash dump generation (max. 3 crash dump files per process).
- **OFF/Empty**: to *disable* crash dump generation.

> **Support:**
>
> If you have followed the instructions above but are unable to **Enable/Disable Crash Dump Generation**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

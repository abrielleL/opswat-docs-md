<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-user-authentication-issues-on-linux -->

# How do I solve User Authentication issues on MetaDefender Endpoint managed Linux devices?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on Linux systems.

Users running MetaDefender Endpoint on one or more Linux devices may occasionally see My OPSWAT Central Management  device compliance warnings/flags related to **User Authentication**, although this depends entirely on policy configurations.

These warnings/flags are triggered by device issues and will appear under **My OPSWAT Central Management Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>User Authentication**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/h738z6sjf0v7q15c0e4aq8b0cpakhro29tg6xxvluhgrvmmwtumd2n4gb046m92l.png)

To remediate authentication-related device compliance issues on managed Linux devices, please follow the instructions below.

> **Please Note:**
>
> The following remediation guidelines were written based on CentOS 7 x64, and the process may vary depending on your distro and version.

## My OPSWAT Central Management Compliance Warning: User Authentication - User Password Protection Is Disabled

1. Click the **Power** icon in the top right-hand corner of the screen and, from the pop-up menu, select **Account Settings**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/q65dvs6i1cftecd27ocrmrwzf276t6j7rumoy4s7sqbrjow9jwy4pso0ynoqofze.png)

2. Click the **Lock**, then enter your **Root** password to unlock the account settings.

![](https://uploads.developerhub.io/prod/97qW/vzdmnarqdn166f936y98gxaleww860ots6ovnw2nt1phk7sp5ydgv4c0tfpxhf3s.png)

3. Click on the **Password** field, then change your **Password**.

![](https://uploads.developerhub.io/prod/97qW/gporcxz79y6ehfemvtdhmx33amm16el6e9311azat7py81aspqbmr7n8veamcsen.png)

4. Once your password has been set, **Restart** the device to apply your settings.

![](https://uploads.developerhub.io/prod/97qW/cx3ssnsgxfdc30ps3ibta0stx7hfloft2v9q4gngabx0muup7n87e2svxri0ib9w.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience User Authentication Issues On Your** **MetaDefender Endpoint Managed Linux Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

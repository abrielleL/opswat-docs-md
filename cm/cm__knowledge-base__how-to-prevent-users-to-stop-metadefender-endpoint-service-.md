<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-to-prevent-users-to-stop-metadefender-endpoint-service- -->

# How to prevent users to stop MetaDefender Endpoint service?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows systems.

> **Pro Tip:**
>
> To help administrators prevent users from stopping the MetaDefender Endpoint service independently, OPSWAT has provided a setting to **hide stop/restart Client service** in the Windows **Services** manager (as illustrated below), which is configurable via the **My OPSWAT Central Management Console.**

![](https://uploads.developerhub.io/prod/1yda/6oltclbv1cgxtd5yylgsyncd0tjz8mui4q8yz0ccrhlhpswtwvttzmprnq9atand.png)

To enable this feature, follow the instructions below.

1. Log into the remote **My OPSWAT Central Management Console**, and navigate to **Settings>Global>Device Agents**.
2. Select the **Require PIN when a user uninstalls agents on a device** option.
3. Input your four-digit shareable **PIN**, then click **Save** to activate your settings, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/1yda/ylywxcrmf76jxwuc9zjn9vjyc7kakvy6ipub0le41njevc0us0gj314xjiqoz4ip.png)

> **Pro Tip:**
>
> The **hide stop/restart** setting will be implemented by the MetaDefender Endpoint after a few minutes, without further action required.
>
> To stop the client service while this setting is enabled, users will need to enter one of the following commands via **Command Prompt** or **Terminal**:
>
> - **GearsAgentService.exe /stop /p <PIN code>**
> - **GearsAgentService.exe /stop**, then input the PIN code as prompted.
>
> Where possible return codes include:
>
> - **0**: Success
>
> **55**: Invalid Parameters

> **Support:**
>
> If you have security concerns or issues around **Preventing Users From Stopping The** **MetaDefender Endpoint** **Service**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

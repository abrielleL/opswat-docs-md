<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-address-os-update-issues-on-opswat-client-metaaccess-am -->

# How do I address OS update issues on MetaDefender Endpoint/My OPSWAT Central Management among managed Windows device?

> **Verify your product compatibility**
>
> This article is applicable to the latest My OPSWAT Central Management Console and API, as well as all MetaDefender Endpoint releases deployed on Windows systems."

My OPSWAT Central Management provides variety compliance options tailored to different operating systems. Specifically for Windows devices, we've implemented a dedicated rule aimed at compelling users to regularly update their operating systems. This involves monitoring the current patching status and detecting any available but uninstalled updates. This proactive approach ensure that system remain current, benefiting from the latest enhancements and security patches, ultimately bolstering device stability and security.

Administrators have the flexibility to determine the frequency at which users are prompted to update their operating system. This can be configured by activating the '**Update(s) have been available**' condition under **Policy > Deep Compliance > Operating System > Windows**, allowing administrators to specify the desired update interval in days. A smaller number indicates a more frequent check for operating system updates.

![](https://uploads.developerhub.io/prod/1yda/ogqtoxc2ugz6tu1et6cfzeh95388dysdfmjxdfn5yxj7d7uulhjsglaavmfku2df.png)

To remediate OS update compliance issues on managed Windows devices, please follow the relevant instructions below.

### Check Windows Update

- Go to Windows Start menu, search for Check for updates, then click in the first results.

![](https://uploads.developerhub.io/prod/1yda/0l1wnl67a0946rlu3m4tqfl06rhrn4asg2li58uozzgncdc04g9spkuc5t7c2szv.png)

- On the Windows Update page, click **Check for updates** to check for available updates**.**

![](https://uploads.developerhub.io/prod/1yda/x5oj2b0e7r3i92x1wyxhc3c74g1chd36tkumdich8udk16x6ir8e1w3hkhvzikh6.png)

- Proceed to download and install the recommended updates. Please note that you may be asked to close all running programs and restart the machine if needed.
- Once the installation is done, open the Windows **Start** menu, search for **MetaDefender Endpoint**, and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/mqg035lzrm0pcvjmo4rzqiw3eapmsdbgsjc6znxibi4n657o0y245pg7nmwh2vdb.png)

- Once the OPSWAT Client is running, right-click on the Client tray icon and click  **Recheck .**

![](https://uploads.developerhub.io/prod/1yda/szx5oe9vy44wea7qiz6tbl4ickwb2vsxeyfhi8x68d1cy9h02x1m4lzgr2t92hso.png)

### Through MetaDefender Endpoint

- Go to the Windows Start menu, search for MetaDefender Endpoint, and select Run as Administrator.

![](https://uploads.developerhub.io/prod/1yda/e6jhzjzerwnova0x0z7gafxr6kd1qond55lp0kgailngtlwtlitf50hztms7jxgo.png)

- On the left panel, click the **OS Updates** section.
- On the  OS Updates page, you will find a list of available OS patches. Click the button on the right side of an update to install it, or click **Update All** to install all updates.

![](https://uploads.developerhub.io/prod/1yda/871x0xm6mpd7ywek5nu20b1b4hmvj4ejdqtmeo39kbdc6xkmqfahmdxwlmgwwy3k.png)

- Once the  installation is done, right-click on the Client tray icon and click **Recheck**.

![](https://uploads.developerhub.io/prod/1yda/7yi1czsorzd4032ex2qn6ip1t254jso0qmjpr8zf6bil7ps0b68l2vy7y1l5d2ah.png)

> **Pro Tip**
>
> If you wish to install new updates automatically, you can use OPSWAT Client’s auto-update feature by switch on the Auto-Update button on the OS Updates page.

### Install OS updates manually

If the above approaches are not working, you may need to download and install the OS updates manually.

1. Go to the Windows Start menu, search for the **winver** command, then click on the first result.

![](https://uploads.developerhub.io/prod/1yda/99nmpp35x4x5hro80zc0grtbsuaio40bb0rbysv6y2bahbmgle7pbrwoeshe3vwn.png)

2. You will find the running OS version and the current build information here.

![](https://uploads.developerhub.io/prod/1yda/tgwsk7gbfzr5529sfis40qq4v9d7ybsaen8ntecljrrs8hnimoi06bl6galy378k.png)

3. Head to the [**Windows release information page**](https://learn.microsoft.com/en-us/windows/release-health/release-information). On the left panel, choose the appropriate release information page based on your running OS (Windows 11, Windows 10, or others).

![](https://uploads.developerhub.io/prod/1yda/3sxq6ctrl9xvld67ccftdkm2g5z4s9btf2bda8rfgm20ecnbyzj6o05e0zhecrok.png)

4. On the release information page, find the section for your OS version. You will see a list of builds under the chosen version. Look for the most recent build and click on the link in the **KB article** column.

![](https://uploads.developerhub.io/prod/1yda/4tpe8a64yr45z5y9wk4z1vxxghhh6pmcre5lwlwbgcpeo8g31get7klblb2p2qkd.png)

5. On the KB page, scroll down to the **How to get this update** section and find the instructions to install the update through the **Microsoft Update Catalog** release channel.

![](https://uploads.developerhub.io/prod/1yda/y0fqb0blf2yer9hp2zcrs0mo6u5k9pw2jiaykjy0qqg91lkti629p9v6zhjzuxm2.png)

6. On the **Microsoft Update Catalog** page, download the appropriate package based on your running OS version and your architecture system.

![](https://uploads.developerhub.io/prod/1yda/id5sfrxzdhdzptkh4jfouu8z8xbm3wociymuaujvmno6gjeh9172xq036mf1h3g0.png)

7. Once the download process is done, double-click on the update package and follow the instructions to install it.
8. Once the installation is done, open the Windows **Start** menu, search for **MetaDefender Endpoint**, and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/61xntga58vbwatd9t8yce3hb2zaelfnw15zmycnoeg8bon287ec3u63iyngzk34u.png)

9. Once the **MetaDefender Endpoint** is running, right-click on the MetaDefender Endpoint tray icon and click **Recheck**.

![](https://uploads.developerhub.io/prod/1yda/2hfrhiea7u0fns9b2ck5c62gh56u86wp6bmlssv99h3oc97szdy1dnpmdrxd3r79.png)

> **Support**
>
> If you have followed the instructions above but **Continue To Experience OS update issues on** **MetaDefender Endpoint / My OPSWAT Central Management** **managed Windows devices**, please open a [**Support Case**](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [**OPSWAT Expert Forum**](https://go2.opswat.com/s).

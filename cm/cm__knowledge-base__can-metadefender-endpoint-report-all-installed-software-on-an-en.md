<!-- source: https://www.opswat.com/docs/cm/knowledge-base/can-metadefender-endpoint-report-all-installed-software-on-an-en -->

# Can MetaDefender Endpoint report all installed software on an endpoint?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux and Android systems.

Yes.

MetaDefender Endpoint is able to detect and report on a wide range of software installed on Windows, macOS and Linux PCs, as well as on Android devices.

Installed software on iOS devices is not reported .

> **Pro Tip:**
>
> The applications currently supported for reporting can be viewed via the links below:
>
> - [Windows](https://software.opswat.com/OESIS_V4/Win/docs/support_charts/support_charts.html)
> - [macOS](https://software.opswat.com/OESIS_V4/Mac/docs/support_charts/support_charts.html)
> - [Linux](https://software.opswat.com/OESIS_V4/Linux/docs/support_charts/support_charts.html)

Administrators can reference a list of all supported installed applications, on all endpoints, in a single view-screen via the **My OPSWAT Central Management Console>Inventory>Applications** page, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/1yda/b2kjhexczz01aav0dmevcnc3hoyee6mb4kurarruomfnbi6ou3yqvw5xxl3ogumy.png)

Administrators can also search for apps using the **Search** field or **Filter** options, as indicated in the screenshots below.

![](https://uploads.developerhub.io/prod/1yda/fxl5j4ujc7jncfr09j7dq8ujngl721erajxefv1mkb2fvsd80gvwk4hdu1h03jux.png)

![](https://uploads.developerhub.io/prod/1yda/2ai1hkmyuimpva7yel3bky0yrnxnxcu51h1l84vrg44ofjqy2xi66fy0qlu9lu09.png)

## Device details view

For a **device details** view of supported installed application reporting, the following applies.

For all operating systems, go to **My OPSWAT Central Management Console>Inventory>Devices>Relevant Device**, as illustrated below.

![](https://uploads.developerhub.io/prod/1yda/pzel8iapso7wamgb79w7524dyo14cvqn0q6r5lpuoenbli93imql7uyd9h9o3hdq.png)

### Windows/macOS

- Security applications are reported under the **Device Compliance** tab.
- Potentially unwanted applications are reported under the **Application Control** and **Other Apps** tabs.
  - On macOS, unwanted application detection is limited to the public file sharing category.
- Other detected software is reported under the **Other** **Apps** tab.
  - This excludes software found under the **Device Compliance** and **Application Control** tabs.
  - Examples include Java, Flash, MS Office, etc.

![](https://uploads.developerhub.io/prod/1yda/wyqggccvxbnkqz4q7dl09inv3d81ftf82o31jb6cax29jdqfb6ubbgy88g8qwt5p.png)

### Linux

- Security applications are reported under the **All Categories** tab.
- Potentially unwanted applications are not reported.
- All installed packages (including security applications) are reported under the **Packages** tab.

![](https://uploads.developerhub.io/prod/1yda/jo88xecm4d5jne9pudwgd09xd80fstyr75jkn2ob72dmj020dk8k2227waoiug08.png)

### Android

- Security applications are not reported.
- Potentially unwanted applications are not reported.
- All installed applications are reported under the **Apps** tab.

> **Support:**
>
> Should you experience any issues regarding **Installed Application Reporting Via the** **MetaDefender Endpoint**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

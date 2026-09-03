<!-- source: https://www.opswat.com/docs/mdendpoint/endpoint-management/can-metadefender-endpoint-report-all-installed-software-on-an-en -->

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

Administrators can reference a list of all supported installed applications, on all endpoints, in a single view-screen via the **MetaDefender IT-OT Access Console>Inventory>Applications** page, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/1yda/d1cvoahbq9ottiwf0sy29szz9j8ddusa7dgvaotxn1io8crhgqhlhuiub7zplurs.png)

![](https://uploads.developerhub.io/prod/1yda/xm7qomapaz8gfx21dj3apjfspqnw0ud1hd500zlgpztb44a845lcy8s8w58z2r15.png)

Administrators can also search for apps using the **Search** field or **Filter** options, as indicated in the screenshots below.

![](https://uploads.developerhub.io/prod/2x2P/dfb968ab7ql97vp6vai98f6h8xa42jsjjpf5i4c9ei8vinuxggxw176dgky8xm8x.png)

## [Device details view](https://docs.opswat.com/macloud-sdp/kb/can-opswat-client-report-all-installed-software-on-an-endpoint-#device-details-view)

For a **device details** view of supported installed application reporting, the following applies.

For all operating systems, go to **MetaDefender IT-OT Access Console>Inventory>Devices>Relevant Device**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/61knip4ur1w15iogut6h72a1fdrvln3qib30cuneisb115iagjfqpuytm6tn2d1j.png)

### [Windows/macOS](https://docs.opswat.com/macloud-sdp/kb/can-opswat-client-report-all-installed-software-on-an-endpoint-#windowsmacos)

- Security applications are reported under the **Device Compliance** tab.
- Potentially unwanted applications are reported under the **Application Control** and **Other Apps** tabs.
  - On macOS, unwanted application detection is limited to the public file sharing category.
- Other detected software is reported under the **Other** **Apps** tab.
  - This excludes software found under the **Device Compliance** and **Application Control** tabs.
  - Examples include Java, Flash, MS Office, etc.

![](https://uploads.developerhub.io/prod/2x2P/uc69s6d82sl91xehkocgd1t5ypto0104stvbh8h83zcfcc0t7irx5gbm424wqa9r.png)

### [Linux](https://docs.opswat.com/macloud-sdp/kb/can-opswat-client-report-all-installed-software-on-an-endpoint-#linux)

- Security applications are reported under the **All Categories** tab.
- Potentially unwanted applications are not reported.
- All installed packages (including security applications) are reported under the **Packages** tab.

![](https://uploads.developerhub.io/prod/2x2P/h7ueev3efpkzmfjxest5dkixiwgblfbdd6wxwtwjlw9pgwswz72w44a98c00881z.png)

### [Android](https://docs.opswat.com/macloud-sdp/kb/can-opswat-client-report-all-installed-software-on-an-endpoint-#android)

- Security applications are not reported.
- Potentially unwanted applications are not reported.
- All installed applications are reported under the **Apps** tab.

> **Support:**
>
> Should you experience any issues regarding **Installed Application Reporting Via the** **MetaDefender Endpoint**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

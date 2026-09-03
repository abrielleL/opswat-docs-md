<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/can-opswat-client-report-all-installed-software-on-an-endpoint- -->

# Can MetaDefender Endpoint report all installed software on an endpoint?

This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux and Android systems.

Yes.

MetaDefender Endpoint is able to detect and report on a wide range of software installed on Windows, macOS and Linux PCs, as well as on Android devices.

Installed software on iOS devices is not reported .

Pro Tip:

The applications currently supported for reporting can be viewed via the links below:

- [Windows](https://software.opswat.com/OESIS_V4/Win/docs/support_charts/support_charts.html)
- [macOS](https://software.opswat.com/OESIS_V4/Mac/docs/support_charts/support_charts.html)
- [Linux](https://software.opswat.com/OESIS_V4/Linux/docs/support_charts/support_charts.html)

Administrators can reference a list of all supported installed applications, on all endpoints, in a single view-screen via the **MetaDefender IT Access Console>Inventory>Applications** page, as illustrated in the screenshot below.

Administrators can also search for apps using the **Search** field or **Filter** options, as indicated in the screenshots below.

## [Device details view](/docs/macloud-sdp/kb/can-opswat-client-report-all-installed-software-on-an-endpoint-#device-details-view)

For a **device details** view of supported installed application reporting, the following applies.

For all operating systems, go to **MetaDefender IT Access Console>Inventory>Devices>Relevant Device**, as illustrated below.

### [Windows/macOS](/docs/macloud-sdp/kb/can-opswat-client-report-all-installed-software-on-an-endpoint-#windowsmacos)

- Security applications are reported under the **Device Compliance** tab.
- Potentially unwanted applications are reported under the **Application Control** and **Other Apps** tabs.

  - On macOS, unwanted application detection is limited to the public file sharing category.
- Other detected software is reported under the **Other** **Apps** tab.

  - This excludes software found under the **Device Compliance** and **Application Control** tabs.
  - Examples include Java, Flash, MS Office, etc.

### [Linux](/docs/macloud-sdp/kb/can-opswat-client-report-all-installed-software-on-an-endpoint-#linux)

- Security applications are reported under the **All Categories** tab.
- Potentially unwanted applications are not reported.
- All installed packages (including security applications) are reported under the **Packages** tab.

### [Android](/docs/macloud-sdp/kb/can-opswat-client-report-all-installed-software-on-an-endpoint-#android)

- Security applications are not reported.
- Potentially unwanted applications are not reported.
- All installed applications are reported under the **Apps** tab.

Support:

Should you experience any issues regarding **Installed Application Reporting Via the** **MetaDefender Endpoint**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

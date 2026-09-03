<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/customizable-reporting -->

# Customizable Reporting

MetaDefender IT Access features the ability to customize and develop reports based on your organization's needs. With the ability to add and delete section, specify groups, and developing a scope of time, administrators can establish personalized reports to their needs and be presented with quick data at a glance.

## [Report Types](/docs/macloud-sdp/configuration---management/customizable-reporting#report-types)

- Account Summary - Provides an overview of the account with data ranging from device health to threat detection.
- Infected Devices - Provides details on devices that are reporting to MetaDefender IT Access as infected.
- SDP Sessions - Provides details on SDP sessions that occur on client devices within the affiliated account.
- Unknown Devices - Provides details on both monitored and unmonitored client devices affiliated with the account.

## [Report Manager - Customizing your report](/docs/macloud-sdp/configuration---management/customizable-reporting#report-manager---customizing-your-report)

The **Report Manager** section within the Reporting tool is available for administrators to review and access their customized reports. Actions such as **Edit, Clone, Delete** are available by selecting the (⋮) by a specific report. Administrators can also choose to activate or deactivate reports based on their needs.

1. Navigate to **Settings > Reports > Report Manager > Create A New Report**
2. Fill out **Name** and select the desired **Device Groups**.
3. Select the **Report Type** and the sections within that type. Administrators must select at least one section to continue creating the report.
4. Choose the **Scope** of the report. Options are Daily, Weekly, Monthly.
5. Input the list of users and emails that should receive the report.
6. Lastly, enter the **Message** that will be attached with the report when sent to designated users.

To review reports created in MetaDefender IT Access, administrators can use the **Filters** available such as **Recurrence** and **Report Type**. This will assist administrators in locating the desired reports within in the **Report Manager**.

## [History](/docs/macloud-sdp/configuration---management/customizable-reporting#history)

Within the reporting manager, administrators are able to review past reports in the **History** tab. This tab records the type of report sent, when it was sent, and to whom it was sent to. Users are also able to view that past report in their browser by selecting the (⋮) by a specific report and select **View**.

In the **History** tab, Administrators are also able to filter and export the historic records of their reports for auditing purposes. To do so:

1. Navigate to **Settings > Reports > History**
2. If filters are required, select **Filters** and select any of the options. Users are able to filter by recurrence and report type.
3. If timeframe is required, select **Timeframe** and select the designated dates.
4. Select **Export CSV** when ready.

## [Download Reports](/docs/macloud-sdp/configuration---management/customizable-reporting#download-reports)

This section of reporting allows administrators to gather CSV files with detailed information generated for the account. The following reports are available for download:

- Device not Reporting - Provides details on devices not reporting into MetaDefender IT Access for the affiliated account based on the 'X' hours value the administrator selects.
- Missing Patches Summary - Provides details on devices that are missing KBs through their designated operating systems.
- Device Missing Specific Patch - Provides details on devices that are missing a specific patch based on the KB number inputted by the administrator.

After selecting the wanted report, and inputting the desired value, administrators can select **Download** to get the CSV file downloaded.

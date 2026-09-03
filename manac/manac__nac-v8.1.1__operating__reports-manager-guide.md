<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/operating/reports-manager-guide -->

# Reports Manager Guide

## [Overview](/docs/manac/nac-v8.1.1/operating/reports-manager-guide#overview)

The purpose of this document is to provide the end user with an overview and basic familiarity with the NAC Reports Manager. The NAC Reports Manager provides a method to visually see trending data.

Access to the features of the NAC Reports Manager will vary depending on the read or write permissions granted to the end user from the User Management section of the NAC Configuration Manager.

## [Introduction](/docs/manac/nac-v8.1.1/operating/reports-manager-guide#introduction)

To access the Reports Manager, navigate to [https://portal.myweblogon.com:8443/manage/#/reports](https://auth.impulse.com:8443/manage/#/reports) . “ [portal.myweblogon.com](http://auth.impulse.com/) ” can be replaced with the IP address of the NAC appliance or the custom hostname of the appliance, if applicable.

Users with “read” access to the Reports Manager will be able to view everything in the Reports Manager. The list of reports can be sorted by clicking on the column titles.

The main window shows all past created reports, their format and the date they were created. The left column contains quick links to show different types of reports.

## [Scheduling Reports](/docs/manac/nac-v8.1.1/operating/reports-manager-guide#scheduling-reports)

Clicking "Schedule Report" in the top right will bring up the page to edit report details. You can change the template, report parameters, report schedule settings and advanced settings of the report type.

Selecting a template will bring up the options for it.

Each type of report has different parameters. The schedule setting options are the same for every report.

The "Preview Report" button will open a page in a new tab from which the report can be viewed, ran, exported, or printed.

Clicking advanced will bring up more options which have default values and do not need to be changed to schedule a report.

| Report Type | Description |
| --- | --- |
| Device History | Displays a comprehensive history of the specified device. The MAC address is the only parameter needed. |
| Device Type - Detail | Displays a details view of a given device type by day within a given IP Filter. The parameters needed are the date, the IP filter and a single device type. |
| Device Type - Summary | Displays a summary of device type counts by day within a given IP Filter. The parameters needed are the IP filter and the device types. |
| Devices Out of Compliance - Detail | Shows device details of out of compliance policies matching a specific IP Filter and Date. The parameters needed are the date, the IP filter and a single policy. |
| Devices Out of Compliance - Summary | Shows Devices that are out of Compliance by day with a breakdown of the Policies that are out of compliance. The parameters needed are the IP filter and the policies. |
| Devices With Policy Key - Detail | Displays a details list of all policy key devices within a specific IP filter for a given day. The parameters needed are the date and the IP filter. |
| Devices With Policy Key - Summary | Shows a breakdown of device type totals (Windows and OS X) by day of the week. The IP filter is the only parameter needed. |
| License Utilization By Day | Shows a daily license utilization total. The date range is the only parameter needed. If Custom is selected, you will need to provide a start and end date. |
| Policy Groups - Detail | Displays device details for a specific policy group, date and IP filter. The parameters needed are the date, the IP filter and a single policy group. |
| Policy Groups - Summary | Displays a summary of Policy Groups that match a specified IP Filter. The parameters needed are the IP filter and the policy groups. |
| Remediated Policies - Detail | Displays device details for a specific policy that has been remediated on a given day and match a specific IP Filter. The parameters needed are the date, the IP filter and a single policy. |
| Remediated Policies - Summary | Displays a summary of Policies that have been remediated by day and match a specific IP Filter. The parameters needed are the IP filter and the policies. |
| User Details | Displays Details about a specific user and devices that have been associated with. The user name is the only parameter needed. |
| Weekly Usage Report | Show various metrics based on the prior weeks usage in order to show where NAC is providing value. Requires no parameters. |

## [Viewing Reports](/docs/manac/nac-v8.1.1/operating/reports-manager-guide#viewing-reports)

Clicking on a report type will open a page showing previously created reports and the details of that type.

Clicking on a report's name will open the PDF file.

- Clicking "Edit" in the top right corner will bring up the page to edit the report details. This is the same page that comes up when first creating a report except it will already have the options filled out.
- Clicking "Delete" will bring up a pop-up to make sure this is what you meant to click. If you click "Delete" again on the pop-up, it will remove the report. The previous runs of this report will still show up in the main Report Manager window.
- Clicking "Preview" will open a page in a new tab from which the report can be viewed, ran, exported or printed.

<!-- source: https://www.opswat.com/docs/cm/endpoint-security-solution/application-control -->

# Application Control

Within **Policies > Endpoint Security > Policy Details**, administrators are given the ability to enable a policy section called **Application Control**.

**Application Control** provides Administrators with the ability to filter out unwanted applications from their client devices. Configurations can apply to both Windows and MacOS devices, and administrators are able to block applications by categories or by specifying the application by name and version number(s).

It is important to note that My OPSWAT Central Management uses MetaDefender Endpoint Security SDK to scan and sort applications into their categories.

## Application Control: Blocking specific applications

To block specific applications, administrators will need to do the following:

1. Navigate to **Policies > Endpoint Security > Select Policy** .
2. Administrators can search device applications in the search bar and select the one they want.
3. By selecting an application, the page will be redirected to a filtered view for the application.
4. To add a 'blocked application' override to a specific category, select the **+** button by the desired category. If the application applies to multiple categories, there is a **click here** link to apply the 'blocked application' override to **all** categories.
5. Once completed, Administrators can also override the other columns to match the desired action and reporting.
6. After adding the override, Administrators can also specify version numbers for that application under the **Version** column. Users can leave this blank to apply to all versions, or use x as a wildcard. Ex: Version 1.x (applies to all version numbers that start with '1').
7. Once completed, save your changes and confirm with your PIN.

An example of blocking specific applications by using OneDrive, which falls under Cloud Storage and Backup:

![](https://uploads.developerhub.io/prod/97qW/jvcyg5rfcaep5dul4tg9d4elwb9jaffuwokt86v73nweg8nbup80cvygkp7h6oup.png)

This example results in My OPSWAT Central Management reading the **Application Control** as:

- Allow all Cloud Storage categorized applications for VMs and servers.
  - BUT, if the application is Microsoft OneDrive, considered this an issue and perform the actions: uninstall and disable for desktops and laptops.
- Allow all Backup categorized applications for all device types

## Application Control: Blocking application categories

1. Navigate to **Policies > Endpoint Security > Policy Details** .
2. Determine what categories of applications you wish to perform activities related to blocking applications. From there, specify what checks you want My OPSWAT Central Management to run (**Installed** or **Running**) and what actions you'd like My OPSWAT Central Management to perform (**Uninstall** or **Delete**).
3. For My OPSWAT Central Management to perform the actions, it must have either/both **Installed** or  **Running** indications checked off. Once either option or both are enabled, administrators can **Uninstall** or **Disable**. Administrators can also mark the categories as critical issues and what device types are relevant to these configurations.
4. If there is a category that an Administrator doesn't need My OPSWAT Central Management to check for, selecting the eye icon can hide the category. At any point, if the categories are needed, Administrators can select **Show inactive categories** and select the eye icon to show them.
5. Once completed, save your changes and confirm with your PIN.

## Application Control: Allowing specific applications

To allow specific applications, administrators will need to do the following:

1. Navigate to **Policies > Endpoint Security > Policy Details** .
2. Administrators can search device applications in the search bar and select the one they want.
3. By selecting an application, the page will be redirected to a filtered view for the application.
4. To add a 'allowed application' override to a specific category, select the **+** button by the desired category. If the application applies to multiple categories, there is a **click here** link to apply the 'allowed application' override to **all** categories.
5. Once completed, Administrators can also override the other columns by disabling the checkmarks to match the desired 'allowed' reporting.
6. After adding the override, Administrators can also specify version numbers for that application under the **Version** column. Users can leave this blank to apply to all versions, or use x as a wildcard. Ex: Version 1.x (applies to all version numbers that start with '1').
7. Once completed, save your changes and confirm with your PIN.

An example of allowing specific applications by using OneDrive, which falls under Cloud Storage and Backup:

![](https://uploads.developerhub.io/prod/97qW/3fxi0zk034pf08m2lv3ru6w1m431nrq54aa2a18olwj2nwd1v6y8rrlzf8ca313a.png)

This example results in My OPSWAT Central Management reading the **Application Control** as:

- Block all Cloud Storage categorized applications for all device types.
  - BUT, if the application is Microsoft OneDrive, then the application is allowed for desktops and laptops.
- Allow all Backup categorized applications for all device types.

## Application Control: Allowing application categories

1. Navigate to **Policies > Endpoint Security > Policy Details** .
2. Determine what categories of applications you wish to add to your allow-list. From there, verify that the category has all columns disabled. If there are certain device types that are allowed to have the applications, while other's aren't, be sure to disable the checks for devices that are *allowed*  to have the application category in question.
3. If there is a category that an Administrator doesn't need My OPSWAT Central Management to check for, selecting the eye icon can hide the category. At any point, if the categories are needed, Administrators can select **Show inactive categories** and select the eye icon to show them.
4. Once completed, save your changes and confirm with your PIN.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)

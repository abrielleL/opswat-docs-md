<!-- source: https://www.opswat.com/docs/cm/configurations/rebranding-package -->

# Rebranding Package

My OPSWAT Central Management now empowers administrators to fully customize the remediation page with the organization's own brand, text for each device group individually. This powerful feature further enhances the end user experience for meeting the strong demands of localization.

> **Warning**
>
> As of December 2022, My OPSWAT Central Management has now released a new style of the remediation package. V2 will be retiring June 2023.  Existing customers will need to manually change to the new look if they have any rebranding customizations.

### Create a rebranding package

1. Log into [My OPSWAT Central Management](https://my.us.opswat.com/signin) console
2. Navigate to the **Settings > Rebranding**
3. Click **Add New Package**
4. Fill in required information
5. Select a rebranding package type you would like to use for this one
   1. Select the remediation style you would like to use. V3 is our latest style
   2. Select the theme you would like to use
   3. You can choose a default package with a specific language
   4. OR you can use your customized package
      1. Download a default package
      2. Customize it by following [Endpoint Remediation Page](https://www.opswat.com/docs/cm/configurations/endpoint-remediation-page) guidelines
      3. Select **Choose File** to upload your customized package. If you get an error, please check again the [Endpoint Remediation Page](https://www.opswat.com/docs/cm/configurations/endpoint-remediation-page) guidelines to make sure you follow guidelines for customization
6. (Recommended step) Preview a remediation page with this package by selecting what remediation page you would like to preview and click Preview In New Tab. A remediation page with a fake data will be opened in a new tab
   1. Access Blocked: a user is blocked from accessing a protected app via IdP
   2. Device At Risk: device has issues
   3. No Issue Found: a device has no issues and is compliant
7. Click **Add** and enter your PIN to create a new rebranding package

![](https://uploads.developerhub.io/prod/97qW/68l6q89bas0rz7hkmx5tuyoy0uzga28i9ws904e9i9iddomck0p0yzmuf0crgslk.png)

### Assign a rebranding package to a group

1. Log into My OPSWAT Central Management console
2. Navigate to the **Inventory > Groups**
3. Select a group you would like to update a rebranding package for remediation pages
4. Navigate to the **Settings** tab
5. Select a rebranding package you would like to assign to the group at the dropdown *Rebranding Package for Remediation Page*
6. Click **Save** and enter your PIN to create a new rebranding package

![](https://uploads.developerhub.io/prod/97qW/vb6g4pycw9m297tndazoqurd874hie94jhod6o9975t6e3e5hyrzc5upx9lcdztb.png)

### Update a rebranding package

1. Log into My OPSWAT Central Management console
2. Navigate to the **Settings > Rebranding**
3. Select a rebranding package you would like to update.
4. Click **Change** next to the package name to update its name.
5. Click **Change** next to the package description to update its description.
6. Switch to "*Use default package*" or "*Customize a package*" if you would like to update rebranding package type.
7. If you would like to upload a customized package, select "Customize a package" option:
   1. download a default package or download the current package if you already uploaded one to this package.
   2. customize it by following guidelines [Endpoint Remediation Page](https://www.opswat.com/docs/cm/configurations/endpoint-remediation-page)
   3. Select **Choose File** to upload your customized package. If you get an error, please check again the [Endpoint Remediation Page](https://www.opswat.com/docs/cm/configurations/endpoint-remediation-page) guidelines to make sure you follow guidelines for customization.
8. (Recommended step) Preview a remediation page with this package by selecting what remediation page you would like to preview and click Preview In New Tab. A remediation page with a fake data will be opened in a new tab.
   1. Access Blocked: a user is blocked from accessing a protected app via IdP.
   2. Device At Risk: device has issues.
   3. No Issue Found: a device has no issues and is compliant.
9. If you make changes in step #6 and #7, click **Save** and enter your PIN to save your changes.

![](https://uploads.developerhub.io/prod/97qW/dzdt70l8ej59lbpzm0hynnm1unc1htejrhqvuvk2p2k3lnw3c8vsscyiktl9mdeq.png)

### Delete a rebranding package

1. Update a rebranding package
2. Navigate to the **Settings > Rebranding**
3. Check on rebranding packages you would like to delete. Note that you can only delete rebranding packages that have not assigned to any device groups yet.
4. Click **Delete**
5. The system will notify you of packages that could not be deleted, if any.
6. Enter your PIN and click **Delete** to confirm your action.

### View what device groups are using a rebranding package

1. Update a rebranding package
2. Navigate to the **Settings > Rebranding**
3. The column 'Groups Assigned' shows how many groups are using a package.
4. Select a rebranding package you would like to view details.
5. Scroll down to the bottom of the page to view what groups are assigned to the selected package.

![](https://uploads.developerhub.io/prod/97qW/g06u914zpglwlqddl24npai1id4kfc13k34h38advan93mqg3n8tqffjqhj8ilsv.png)

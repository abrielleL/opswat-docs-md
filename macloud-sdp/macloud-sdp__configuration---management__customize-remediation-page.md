<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/customize-remediation-page -->

# Rebranding Package

MetaDefender IT Access now empowers administrators to fully customize the remediation page with the organization's own brand, text for each device group individually. This powerful feature further enhances the end user experience for meeting the strong demands of localization.

Warning

As of December 2022, MetaDefender IT Access has now released a new style of the remediation package. V2 will be retiring June 2023. Existing customers will need to manually change to the new look if they have any rebranding customizations.

### [Create a rebranding package](/docs/macloud-sdp/configuration---management/customize-remediation-page#create-a-rebranding-package)

1. Log into MetaDefender IT Access console.
2. Navigate to the **Settings > Rebranding**
3. Click **Add New Package**.
4. Fill in required information.
5. Select a rebranding package type you would like to use for this one

   1. Select the remediation style you would like to use. V3 is our latest style.
   2. Select the theme you would like to use.
   3. You can choose a default package with a specific language.
   4. OR you can use your customized package.

      1. Download a default package.
      2. Customize it by following guidelines [here](/docs/macloud-sdp/configuration---management/customize-remediation-page-guideline).
      3. Select **Choose File** to upload your customized package. If you get an error, please check again the [guideline](/docs/macloud-sdp/configuration---management/customize-remediation-page-guideline) to make sure you follow guidelines for customization.
6. (Recommended step) Preview a remediation page with this package by selecting what remediation page you would like to preview and click Preview In New Tab. A remediation page with a fake data will be opened in a new tab.

   1. Access Blocked: a user is blocked from accessing a protected app via IdP.
   2. Device At Risk: device has issues.
   3. No Issue Found: a device has no issues and is compliant.
7. Click **Add** and enter your PIN to create a new rebranding package.

### [Assign a rebranding package to a group](/docs/macloud-sdp/configuration---management/customize-remediation-page#assign-a-rebranding-package-to-a-group)

1. Log into MetaDefender IT Access console
2. Navigate to the **Inventory > Device Groups**
3. Select a group you would like to update a rebranding package for remediation pages
4. Navigate to the **Settings** tab
5. Select a rebranding package you would like to assign to the group at the dropdown *Assigned Rebranding Package*.
6. Click **Save** and enter your PIN to create a new rebranding package

### [Update a rebranding package](/docs/macloud-sdp/configuration---management/customize-remediation-page#update-a-rebranding-package)

1. Log into MetaDefender IT Access console.
2. Navigate to the **Settings > Rebranding**
3. Select a rebranding package you would like to update.
4. Click **Change** next to the package name to update its name.
5. Click **Change** next to the package description to update its description.
6. Switch to "*Use default package*" or "*Customize a package*" if you would like to update rebranding package type.
7. If you would like to upload a customized package, select "Customize a package" option:

   1. download a default package or download the current package if you already uploaded one to this package.
   2. customize it by following guidelines [here](/docs/macloud-sdp/configuration---management/customize-remediation-page-guideline).
   3. Select **Choose File** to upload your customized package. If you get an error, please check again the [guideline](/docs/macloud-sdp/configuration---management/customize-remediation-page-guideline) to make sure you follow guidelines for customization.
8. (Recommended step) Preview a remediation page with this package by selecting what remediation page you would like to preview and click Preview In New Tab. A remediation page with a fake data will be opened in a new tab.

   1. Access Blocked: a user is blocked from accessing a protected app via IdP.
   2. Device At Risk: device has issues.
   3. No Issue Found: a device has no issues and is compliant.
9. If you make changes in step #6 and #7, click **Save** and enter your PIN to save your changes.

### [Delete a rebranding package](/docs/macloud-sdp/configuration---management/customize-remediation-page#delete-a-rebranding-package)

1. Log into MetaDefender IT Access console.
2. Navigate to the **Settings > Rebranding**
3. Check on rebranding packages you would like to delete. Note that you can only delete rebranding packages that have not assigned to any device groups yet.
4. Click **Delete**
5. The system will notify you of packages that could not be deleted, if any.
6. Enter your PIN and click **Delete** to confirm your action.

### [View what device groups are using a rebranding package](/docs/macloud-sdp/configuration---management/customize-remediation-page#view-what-device-groups-are-using-a-rebranding-package)

1. Log into MetaDefender IT Access console.
2. Navigate to the **Settings > Rebranding**
3. The column 'Groups Assigned' shows how many groups are using a package.
4. Select a rebranding package you would like to view details.
5. Scroll down to the bottom of the page to view what groups are assigned to the selected package.

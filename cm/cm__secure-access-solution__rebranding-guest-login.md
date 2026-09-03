<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/rebranding-guest-login -->

# Rebranding Guest login

My OPSWAT Central Management enables administrators to personalize the web login page with their organization's branding and custom text for each device group. This feature enhances the user experience and supports localization needs.

### Create a rebranding package

1. Log into My OPSWAT Central Management console.
2. Navigate to the **Settings > Rebranding**
3. Click **Add New Package**.
4. Fill in required information.
5. Select a rebranding package type you would like to use for this one
   1. Select the remediation style you would like to use. V3 is our latest style.
   2. Select the theme you would like to use.
   3. Select the option to use your customized package.
      1. Download a default package.
      2. Customize it by following guidelines [Customize Guest login](https://www.opswat.com/docs/cm/secure-access-solution/customize-guest-login).
      3. Select **Choose File** to upload your customized package. If you get an error, please check again the [Customize Guest login](https://www.opswat.com/docs/cm/secure-access-solution/customize-guest-login) to make sure you follow guidelines for customization.
6. (Recommended step) Preview a remediation page with this package by selecting what remediation page you would like to preview and click Preview In New Tab. A remediation page with a fake data will be opened in a new tab.
   1. Access Blocked: a user is blocked from accessing a protected app via IdP.
   2. Device At Risk: device has issues.
   3. No Issue Found: a device has no issues and is compliant.
7. Click **Add** and enter your PIN to create a new rebranding package.

### Assign a rebranding package to Guest Login page

1. Log into My OPSWAT Central Management console
2. Navigate to the **User Management > RADIUS NAC > Guest Registration Setting**
3. Select a rebranding package you would like to assign to the group at the dropdown *Assigned Rebranding Package*.
4. Click **Save** and enter your PIN.

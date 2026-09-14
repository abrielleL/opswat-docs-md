<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/configuration/centralized-scanning-profile -->

# Centralized Scanning Profile

MetaDefender Drive administrators can now lock drives using MetaDefender Drive Toolkit (starting at v3.7.0) and require only OTP-authorized users to perform restricted actions.

On locked drives, Operators are required to obtain a 6-digit One Time Password (OTP) from a user assigned an Approver role in order to perform any of the restricted actions, such as a quick scan, custom scan or any ad-hoc field policy modification.

With this new feature, the MetaDefender Drive provisioning process includes three user roles:

- **Administrators:** Responsible for provisioning the MetaDefender Drive using the Drive Toolkit.
- **Approvers:** Assigned by Administrators to authorize Operators to use locked drives; they do not interact physically with drives.
- **Operators**: Physically use the MetaDefender Drive to perform scanning operations.

Info

This feature isn't mandatory. If you don't enroll a device, it can be used by any field operator who has physical access to it.

## [**Administrator Provisioning**](/docs/mddrive/v4.4.2a/configuration/centralized-scanning-profile#administrator-provisioning)

### [Enrollment and Lock MetaDefender Drive](/docs/mddrive/v4.4.2a/configuration/centralized-scanning-profile#enrollment-and-lock-metadefender-drive)

After booting MetaDefender Drive to be enrolled, the administrators open MetaDefender Drive Toolkit.

1. Go to **Settings tab**
2. Select **Lock MD Drive Software**
3. Click **Set up Lock**

Install the Google Authentication Application to generate a 6-digit OTP (one-time password).

### [Assign an Approver](/docs/mddrive/v4.4.2a/configuration/centralized-scanning-profile#assign-an-approver)

Enter a name to identify the Approver, then click Add

Enter the MetaDefender Drive credentials (Account Name and Your Key) into the Google Authenticator app for secure OTP generation.

A pop-up will confirm successfully locking MetaDefender Drive.

### [Unenrollment for MetaDefender Drive](/docs/mddrive/v4.4.2a/configuration/centralized-scanning-profile#unenrollment-for-metadefender-drive)

After booting the MetaDefender Drive the administrators wish to unenroll:

1. Go to **Settings tab**
2. Select **Lock MD Drive Software**
3. Click on **icon**

Administrators can directly unenroll on Drive Toolkit by clicking **Unenroll Device**

Click **Yes**

A prompt will appear upon completion.

## [Approver](/docs/mddrive/v4.4.2a/configuration/centralized-scanning-profile#approver)

Assigned by the Administrator to authorize Operators to unlock MetaDefender Drive. Administrators can also perform the Approver role.

Info

Approvers need to install Google Authenticator application on their device to generate 6-digit OTP for remote authorization.

An approver receives a one-time password via Google Authenticator to authorize scan configuration changes. The approved request is then sent to the operator to apply the ad-hoc modifications.

The input screen for one-time passcode approval now clearly shows the last 6 digits of the MetaDefender Drive ID long with the Approver's name, for faster local scan change approval.

*The input screen for one-time passcode on MetaDefender Drive*

**Operator Authorization**

As a MetaDefender Drive Operator, once the MetaDefender Drive is enrolled, you will be restricted from performing **Quick** and **Custom** scans. You can only perform a **Full Scan** and **Update Engine Version**.

**Ad-hoc configuration changes** are required to obtain a 6-digit One Time Password (OTP) from a user who was assigned an Approver role in order to perform any of the restricted actions, such as a quick scan or custom scan.

1. To check if your Drive is locked, You can go to the **Scan** page, or the Engines page to see if there are restricted actions.

Scan options on a locked Drive

2. To unlock your Drive, click any of the restricted actions. You will be prompted to enter a 6-digit authentication code.

3. Ask the Approver for the Drive you are using to provide you with an updated authentication code using their Google Authenticator app, then enter this code and click **Verify**.

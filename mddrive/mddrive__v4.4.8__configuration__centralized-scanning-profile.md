<!-- source: https://www.opswat.com/docs/mddrive/v4.4.8/configuration/centralized-scanning-profile -->

# Centralized Scanning Profile

MetaDefender Drive administrators can now lock drives using MetaDefender Drive Toolkit (starting at v3.7.0) and require only OTP-authorized users to perform restricted actions.

On locked drives, Operators are required to obtain a 6-digit One Time Password (OTP) from a user assigned an Approver role in order to perform any of the restricted actions, such as a quick scan, custom scan or any ad-hoc field policy modification.

With this new feature, the MetaDefender Drive provisioning process includes three user roles:

- **Administrators:** Responsible for provisioning the MetaDefender Drive using the Drive Toolkit.
- **Approvers:** Assigned by Administrators to authorize Operators to use locked drives; they do not interact physically with drives.
- **Operators**: Physically use the MetaDefender Drive to perform scanning operations.

Info

This feature isn't mandatory. If you don't enroll a device, it can be used by any field operator who has physical access to it.

Follow instructions bellow to set up and make use of **Centralized Scanning Profile**:

- [Centralized Scanning Profile - Provisioning from Drive Toolkit](/docs/mddrive/v4.4.8/configuration/centralized-scanning-profile-provision-from-toolkit)
- [Centralized Scanning Profile - Provisioning from Smart Touch](/docs/mddrive/v4.4.8/configuration/centralized-scanning-profile-provision-from-smart-touch)
- [Centralized Scanning Profile - Unlock in MetaDefender Drive](/docs/mddrive/v4.4.8/configuration/centralized-scanning-profileqno)

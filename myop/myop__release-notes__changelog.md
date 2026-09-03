<!-- source: https://www.opswat.com/docs/myop/release-notes/changelog -->

# Changelog

## [Version 2025.2.1-OP](/docs/myop/release-notes/changelog#version-202521-op)

Release date: April 12, 2025, UTC

**Product Management:**

- Version: 2025.2.1
- Detailed release notes can be found [here](https://www.opswat.com/docs/product-management/v2025.2.1/get-started/user-guide).

**Known Limitations:**

- Import/Export limit
- Upgrading via the Upgrade My OPSWAT function does not update the new system requirements for the virtual appliance.

## [Version 2025.1.1-OP](/docs/myop/release-notes/changelog#version-202511-op)

Release date: January 17, 2025, UTC

**Product Management:**

- Version: 2024.4.5
- Detailed release notes can be found [here](https://www.opswat.com/docs/product-management/v2025.1.2/release-notes).

**New Features:**

- Password complexity policy.

**Enhancements:**

- Additional CLI commands.
- Entity ID attribute for SSO user directories.
- Enhanced IP address configuration script.
- Improved user experience and interface.

**Bugs Fixed:**

- Inventory dashboard could not loaded on the first login session after upgrading the My OPSWAT server.

**Known Limitations:**

- Import/Export limit
- Upgrading via the Upgrade My OPSWAT function does not update the new system requirements for the virtual appliance.

## [Version 2024.4.3-OP](/docs/myop/release-notes/changelog#version-202443-op)

Release Date: December 12, 2024, UTC

**Product Management:**

- Version: 2024.4.5
- Detailed release notes can be found [here](https://www.opswat.com/docs/product-management/v2024.4.5/release-notes).

**New Features:**

- Export users/groups

**Enhancements:**

- Upgrade My OPSWAT software only.
- Improved user experience and interface.

**Bugs Fixed:**

- Active Directory users cannot log in if the user directory's configuration uses a lowercase "dc" in the **User Base DN** or **Group Base DN** fields.
- Usernames were not treated as case-insensitive.
- The current My OPSWAT version was displayed as N/A.

**Known Limitations:**

- Import/Export limit
- Upgrading via the Upgrade My OPSWAT function does not update the new system requirements for the virtual appliance.
- Users cannot log in if all local User Directories have been removed.

## [Version 2024.4.2-OP](/docs/myop/release-notes/changelog#version-202442-op)

Release Date: November 6, 2024, UTC

**Product Management:**

- Version: 2024.4.3
- Detailed release notes can be found [here](https://docs.opswat.com/product-management/v2024.4.3/release-notes/release-notes).

**New Features:**

- PIN requirement for change activities

**Enhancements:**

- Improved user experience and interface.

**Bugs Fixed:**

- Users cannot log in if all local User Directories have been removed.
- After upgrading My OPSWAT, all secret tokens used to authenticate with Public APIs were invalidated.
- When changing the Secure Connection or Proxy settings, the save button was not enabled.

**Known Limitations:**

- Import/Export limit
- Upgrading via the Upgrade My OPSWAT function does not update the new system requirements for the virtual appliance.
- Users cannot log in if all local User Directories have been removed.

## [Version 2024.4.1-OP](/docs/myop/release-notes/changelog#version-202441-op)

Release Date: October 17, 2024, UTC

**Product Management:**

- Version: 2024.4.1
- Detailed release notes can be found [here](https://docs.opswat.com/product-management/v2024.4.1/release-notes/release-notes).

**Bugs Fixed:**

- My OPSWAT On-premises offline license could not be activated.

**Known Limitations:**

- Import/Export limit
- Upgrading via the Upgrade My OPSWAT function does not update the new system requirements for the virtual appliance.
- Users cannot log in if all local User Directories have been removed.

## [Version 2024.3.3-OP](/docs/myop/release-notes/changelog#version-202433-op)

Release Date: September 18, 2024, UTC

**Product Management:**

- Version: 2024.3.4
- Detailed release notes can be found [here](https://docs.opswat.com/product-management/v2024.3.4/release-notes/release-notes).

**New Features:**

- Custom user roles

**Enhancements**:

- Improved Email configuration
- Static IP address configuration
- Disk storage extension
- Low disk storage alert
- Module updates
- Updated user interface

**Bugs Fixed:**

- No events were recorded in Events History for certain events such as configuration changes to a SSO user directory or changing Secure Connection settings.
- Scan reports could not be imported for a pre-enrolled product instances.
- MetaDefender Kiosk L-Series instances could not download firmware update file from My OPSWAT On-premises.
- Users and groups from Active Directory could be added multiple times as duplicates.
- In Module Updates, the option "Delete files after import" for Folder update mode did not work correctly.
- Active Directory users could not log in after an invalid Active Directory user group was added.
- Active Directory user group did not transitioned from Invited to Active status even after a user from this group had logged in successfully.

**Known Limitations:**

- Import/Export limit
- Unenrolled product instances after upgrading My OPSWAT On-premises via Upgrade My OPSWAT.
- Upgrading via the Upgrade My OPSWAT function does not update the new system requirements for the virtual appliance.
- Users cannot log in if all local User Directories have been removed.

## [Version 2024.3.1-OP](/docs/myop/release-notes/changelog#version-202431-op)

Release Date: July 05, 2024, UTC

**Product Management:**

- Version: 2024.3.1
- Detailed release notes can be found [here](https://docs.opswat.com/product-management/v2024.3.1/release-notes/release-notes)

**Bugs Fixed:**

- Changes to Trust Certificates were not properly propagated to all My OPSWAT On-premises services, causing some outgoing connections to fail, such as when using a HTTPS proxy with a self-signed certificates.
- After an IP address change for the virtual appliance, product reports' download URLs did not change to match the new address.
- MetaDefender Kiosk L-Series instances failed to download the firmware update package from My OPSWAT On-premises.
- MetaDefender Kiosk L-Series instances failed to enroll with an "Issue with license" error if the My OPSWAT On-premises server used an offline license for this product type.
- View-Only users could perform certain actions that should be out of View-Only permission scope
- Upgrade My OPSWAT recurrence setting was always set to 1 hour.
- Could not delete a certificate if it was the only certificate added to the My OPSWAT On-premises server.

**Other Changes:**

- The Virtual Appliance Minimum Requirements has been revised

**Known Limitations:**

- Import/Export limit
- Unenrolled product instances after upgrading My OPSWAT On-premises via Upgrade My OPSWAT.
- Upgrading via the Upgrade My OPSWAT function does not update the new system requirements for the virtual appliance.
- Users cannot log in if all local User Directories have been removed.

## [Version 2024.2.2-OP](/docs/myop/release-notes/changelog#version-202422-op)

Release Date: June 6, 2024, UTC

**New Features:**

- Login attempts policy for Local user directory
- Import/Export

**Enhancements:**

- Editing user directories of the Active Directory type no longer requires administrator to re-enter the Active Directory credentials.
- Updated user interface
- Auto-synchronize time with a public NTP server

**Bugs Fixed:**

- When logged in as the same user in multiple browsers/systems, all user sessions got logged out if just one session reached the timeout limit.
- Users that belong to an Active Directory/SSO user directory whose permission had recently been assigned from Administrator to View-Only permission could still make changes to the user directory.

Version 2024.2.1-beta

Release Date: April 3, 2024

**New Features:**

- Proxy settings
- Email settings
- Certificates settings
- Upgrade My OPSWAT

**Enhancements:**

- User Management
- Update settings for OPSWAT Products

**Other Changes:**

- Removed Module Updates settings

## [Version 2023.4.4-beta](/docs/myop/release-notes/changelog#version-202344-beta)

Release Date: Jan 22, 2024, UTC

**New Features:**

- On-premises version of My OPSWAT
- Product Management
- Secure Connection
- Proxy settings

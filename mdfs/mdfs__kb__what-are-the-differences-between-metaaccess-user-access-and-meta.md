<!-- source: https://www.opswat.com/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta -->

# What are the differences between MetaAccess User Access and MetaDefender User Access in Permission Sets?

## [Overview](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#overview)

When MetaDefender for Salesforce is installed, it adds the following permission sets to your Salesforce organization:

- MetaDefender User Access
- MDFS Admin Access (called "CSFS Admin Access" in older versions)
- Approver
- MetaAccess User Access (legacy, no longer used)

The app assigns these permission sets automatically in the background, so in most cases you do not need to assign them manually.

Although both are automatically assigned to all users in your Salesforce organization, they serve different purposes and require different license types.

## [Understanding MetaAccess User Access and MetaDefender User Access Permission Sets in Salesforce](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#understanding-metaaccess-user-access-and-metadefender-user-access-permission-sets-in-salesforce)

### [1. MetaDefender User Access](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#1-metadefender-user-access)

**Purpose** Allows a user to use MetaDefender. Every user whose uploaded files should be scanned needs this permission set. Without it, files uploaded by that user are not scanned, and the MetaDefender log shows: "Failed to upload the file. Uploader doesn't have MetaDefender permission."

**Key Capabilities Enabled**

- Multiscanning: scans files with multiple leading anti-malware engines for high detection accuracy.
- Deep Content Disarm and Reconstruction (Deep CDR): sanitizes and regenerates common file types uploaded to Salesforce, protecting against file-based attacks.
- Proactive DLP: detects and blocks sensitive, out-of-policy and confidential data within files.
- Adaptive Sandbox: detects and analyzes malware by observing its behavior in an emulated environment.
- Reputation checks: checks links and other data in Salesforce records against MetaDefender Cloud threat intelligence.
- Blocking and release requests: blocks infected files and lets users request their release.

**Note:** Users on restricted Salesforce licenses (for example Guest, Chatter Free, Chatter External, or community/portal users) cannot receive this permission set. Their uploads are handled by the app automatically and do not require it.

### [2. MDFS Admin Access](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#2-mdfs-admin-access)

**Purpose**

Gives access to the OPSWAT app, the OPSWAT Settings, the MetaDefender logs, system logs and the MetaDefender dashboard. Users with this permission set appear in OPSWAT Settings > Admin Settings > MDFS Admins.

#### [How it is assigned](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#how-it-is-assigned)

The app automatically gives MDFS Admin Access to a user when:

- the user's profile has the "View All Data" permission (for example System Administrator, or any custom profile with similar admin rights), or
- the user is selected in OPSWAT Settings > Admin Settings > Approvers.

### [3. Approver](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#3-approver)

#### [Purpose](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#purpose)

Allows a user to approve or reject requests to release files that MetaDefender has blocked. It is assigned to users selected in OPSWAT Settings > Admin Settings > Approvers. These users also receive MDFS Admin Access.

### [4. MetaAccess User Access (legacy)](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#4-metaaccess-user-access-legacy)

This permission set belonged to the MetaAccess device compliance integration, which is no longer used. It is still included in the package, but the app does not assign it, and it is not needed for MetaDefender file scanning.

#### [Automatic permission assignment](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#automatic-permission-assignment)

A background job runs on a schedule (every 30 minutes by default) and once after the app is installed or upgraded. Each time it runs, it:

- looks at active users who do not have MetaDefender User Access yet (integration and automated process users are skipped),
- only includes users created within the configured number of days,
- assigns MetaDefender User Access, and MDFS Admin Access / Approver where the rules above apply.

The job only adds permission sets. It never removes them.

You can control this in OPSWAT Settings > User Permission Assignment Settings:

- Configure Permission Assignment Schedule (in Hours): how often the job runs. Default: every 30 minutes.
- Configure Permissions for Users Created Before X Days: only users created within the last X days are included. Default: 1 day. If set to 0, all active users are included.
- Configure Permission Assignment for Certain Profiles: when enabled, permissions are assigned automatically only to users with the selected profiles (up to 50). Users with other profiles do not receive MetaDefender User Access automatically and must be assigned it manually, otherwise their files are not scanned.
- Configure Permissions for Users in selected profiles before X days: the same day limit as above, used when "Certain Profiles" is enabled. Default: 1 day.

Note: "Enable Scan Only For Certain Profiles" (Scan Settings tab) is a different setting. It controls whose files are scanned, not who receives permission sets.

Info: If further assistance is required, please log a support case or chat with our support engineers.

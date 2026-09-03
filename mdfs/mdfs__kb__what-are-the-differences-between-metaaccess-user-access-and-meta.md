<!-- source: https://www.opswat.com/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta -->

# What are the differences between MetaAccess User Access and MetaDefender User Access in Permission Sets?

## [Overview](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#overview)

When OPSWAT’s MetaDefender for Salesforce installed, they create two key permission sets:

- **MetaAccess User Access**
- **MetaDefender User Access**

These permission sets are automatically assigned to all users, ensuring consistent security coverage across your Salesforce organization.

Although both are automatically assigned to all users in your Salesforce organization, they serve different purposes and require different license types.

## [Understanding MetaAccess User Access and MetaDefender User Access Permission Sets in Salesforce](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#understanding-metaaccess-user-access-and-metadefender-user-access-permission-sets-in-salesforce)

### [1. MetaAccess User Access](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#1-metaaccess-user-access)

**Purpose** Grants users access to OPSWAT’s MetaAccess integration, which checks the security posture of devices before allowing them to access Salesforce.

**Key Capabilities Enabled**

- Device compliance verification before login or data access.
- Enforcement of OPSWAT MetaAccess policies.
- Prevention of non-compliant devices from accessing sensitive Salesforce records.

### [2. MetaDefender User Access](/docs/mdfs/kb/what-are-the-differences-between-metaaccess-user-access-and-meta#2-metadefender-user-access)

**Purpose**

Grants access to the MetaDefender Cloud, which scans and sanitizes files to prevent malicious or sensitive data from entering Salesforce.

**Key Capabilities**

- **Multiscanning Technology:** Uses up to 15 leading anti-virus engines for high detection accuracy.
- **Deep Content Disarm and Reconstruct (CDR):** Scans, sanitizes, and regenerates over 175 common file types uploaded to the Salesforce environment, ensuring maximum protection against filebased attacks
- **Proactive DLP:** Detects and blocks sensitive, out-of-policy, and confidential data within files and emails.
- **Adaptive Sandbox:** Detects and analyzes malware by exposing and recording malicious behavior in an emulated environment
- **Infected File Notifications:** Sent in-app and via email to ensure administrators are immediately informed of any infected files.
- **Centralized Control and Visualization Report:** Provides a dynamic dashboard with complete visibility, real-time reports, and management tools in one interface

Note: Administrators can manage the **Permission Assignment Schedule** to control when and how permissions are assigned to specific user profiles. This provides greater flexibility and granularity in permission management, and to protect the Salesforce Apex governor limits.

From OPSWAT Settings:

Info

Please note that “MetaAccess User Access” and> “MetaDefender User Access” require different license types. For more details or> to purchase additional licenses, please contact your Sales representative.

Info

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

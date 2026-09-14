<!-- source: https://www.opswat.com/docs/mddrive/release-notes/release-note-v4-3-0 -->

# MetaDefender Drive v4.3.0

|  |  |  |
| --- | --- | --- |
| **Released on Mar 14, 2025** | A major release introducing new features, and enhancements. |  |
| **New Feature** | MetaDefender Drive now supports **Centralized** **Scanning Profile**, ensuring policy consistency while allowing **on-site scanning policy modifications** with **remote** **approval** using a one-time password (OTP). To enable this feature, users **must** [set the BIOS time](https://www.opswat.com/docs/mddrive/configuration/configuring-bios-time-for-managed-scanning-profile) **to the current time in the UTC+0 time zone.**  **Ad-hoc Configuration Changes**: A Field Operator can locally modify scanning policies on an enrolled MetaDefender Drive, with remote approval from an Administrator or Approver via a one-time password (OTP) through Google Authenticator application.    *An approver receives a one-time password via Google Authenticator to use for authorizing scan configuration modifications.*    *Field Operator input one-time-password from Approver for any scan configuration change requests.*  **Policy Enforcement**: Enrolled MetaDefender Drive devices can only update engines and perform full scans, streamlining scanning operations. |  |
| **Enhancements** | - **Selective Report Sync**: Users can now manually choose which reports to sync with OPSWAT Central Management, providing greater control over report management. - **Optimized Support Package:** The support package size has been reduced from 4–12GB to 2–6GB, accelerating troubleshooting and minimizing upload time. |  |

##

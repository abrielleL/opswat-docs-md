<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/display-imminent-issues-remediation-page -->

# Display Imminent Issues

Administrators now have the option to display imminent issues on the remediation page. **Imminent issues** are potential compliance problems that, although not currently affecting the system, could impact the compliance status of end-user machines in the near future if left unaddressed.

By highlighting these imminent issues, end-users are informed about their machine's security status and can take proactive measures to resolve any impending problems. This proactive approach helps prevent disruptions in access to resources protected by MetaDefender IT Access and ensures continued compliance.

To enable this feature, administrators can follow these steps:

1. Log into the MetaDefender IT Access console and navigate to **Settings > Rebranding.**
2. Select a rebranding package you would like to update.
3. You will see the option to “**Display imminent issues”** in the **Display** section.
4. Make the needed changes and click **Save.**

(*): *To prevent confusion among end-users, we display imminent issues on the remediation page only when they are about to become actual issues soon. For example, suppose a compliance check requires users to perform a backup every 10 days. In that case, we will show the imminent issue only for users who have not backed up their devices in the last 7 days, indicating that their devices will have a backup issue in 3 days if they neglect the backup.*

When enabled, MetaDefender IT Access will display the imminent issues in the **Imminent** section on the remediation page. On the right side of each imminent issue, end-users will see the time left to resolve it before it changes to an actual one and affects the machines' compliance status.

The imminent issues display feature supports only the policy compliance checks listed below

- **Anti-Malware**

  - Signature definition is updated at least every [N] day(s)
  - No full system scan completed in the last [N] day(s)

- **Backup**

  - No backup activity within the last [N] day(s)

- **Operating System**

  - Update(s) have been available for [N] day(s) or more
  - Device has not been rebooted in over [N] day(s)

- **Security & Health (Mobile)**

  - Device has not been rebooted in over [N] day(s)

- **Vulnerabilities and Exposures**

  - Device has CVEs match the conditions below: CVEs with [severity level] for [N] day(s) or more

- **Patch Management**

  - Patch management agent has reported: [Any/Required missing patches] in [all categories/the following category] with [all/specific severity level] : [critical, important, moderate, low] over [N] day(s)

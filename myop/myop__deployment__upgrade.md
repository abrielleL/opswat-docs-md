<!-- source: https://www.opswat.com/docs/myop/deployment/upgrade -->

# Upgrade My OPSWAT

My OPSWAT On-premises provides two upgrade options:

- Virtual appliance upgrade: only applicable to deployments that deployed My OPSWAT On-premises as a virtual appliance. This option updates both the operating system and My OPSWAT software.
- Software-only upgrade: This option updates only My OPSWAT On-premises software.It's recommended for deployments using an AWS AMI image or an Azure virtual machine.

In this section, administrators can configure the upgrade behavior of MyOPSWAT On-premises.

The following option(s) are currently available:

**Update Source:**

- **Manual**: Administrators need to download an appropriate upgrade package from [My OPSWAT Portal](my.opswat.com) and manually upload the files through My OPSWAT On-premises console to upgrade.

  - **Import file to update:** Open the file browser to select the update files.
  - **Update Now:** Click to start the upload process for the update files.

Update Now

Please note that the update files are only uploaded to My OPSWAT On-premises once **Update Now** is clicked.

The firmware upgrade process for My OPSWAT On-premises will start immediately once the update files are completely uploaded. We recommend that you take a snapshot backup of the virtual appliance before clicking **Update Now**.

- **Internet:** My OPSWAT On-premises periodically checks with OPSWAT servers to fetch the latest update files.

  - **Recurrence Pattern:** Minutely/Hourly/Daily/Weekly/Monthly.
  - **Recur every:** Select the update frequency depending on the selected recurrence pattern.

Info

When My OPSWAT starts the upgrade process, active users will see a popup to tell the users to save changes if any.

Changed SSH host key after upgrade

Due to how the virtual appliance's operating system is upgraded, the host SSH key will be changed after the upgrade process completes.

You may receive an error message when connecting to the virtual appliance via SSH with the strict host checking option (enabled by default).

Known Limitations: Unenrolled product instances after upgrading

For certain product types such as MetaDefdender Core, after upgrading, their instances may become unenrolled if My OPSWAT On-premises does not have [HTTPS mode](/docs/myop/configuration/secure-connection#enabling-https) enabled.

**Workaround:** To avoid this issue, please enable [HTTPS mode](/docs/myop/configuration/secure-connection#enabling-https) before upgrading.

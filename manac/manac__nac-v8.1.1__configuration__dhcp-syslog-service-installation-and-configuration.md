<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/dhcp-syslog-service-installation-and-configuration -->

# DHCP Syslog Service Installation and Configuration

## [DHCP Syslog Services Prerequisites](/docs/manac/nac-v8.1.1/configuration/dhcp-syslog-service-installation-and-configuration#dhcp-syslog-services-prerequisites)

The following prerequisites will need to be completed on all Windows DHCP servers used by machines being managed by NAC.

## [Step-by-step guide](/docs/manac/nac-v8.1.1/configuration/dhcp-syslog-service-installation-and-configuration#step-by-step-guide)

## [Confirm Log File Size](/docs/manac/nac-v8.1.1/configuration/dhcp-syslog-service-installation-and-configuration#confirm-log-file-size)

Ensure the value allows for sufficient log file growth. NAC needs to relay all DHCP transactions to NAC. If the log file growth is capped, the DHCP server will stop logging and NAC will not receive the transactions.

- Open the registry to confirm this by locating the one of the following keys:

Windows 2008 and Windows 2012:

HKLM\SYSTEM\CurrentControlSet\Services\DhcpServer\Parameters\DhcpLogFilesMaxSize

Some Windows 2008:

HKLM\SYSTEM\CurrentControlSet\Services\DhcpServer\Parameters\DhcpLogMinSpaceOnDisk

Note: Windows Servers will only have one of these registry keys. Do not create an additional registry key if one is already present.

- NAC recommends setting this to a value equal to 2048MB (if represented as a hex value it would be "800")

  - This will allow for 7 (seven) 290 MB log files.
  - Note: Every environment is different. NAC recommends 700 MB as a starting point. A larger environment may generate a higher volume of DHCP Transaction Logs, if the log files stop being updated during the week, this value will need to be increased.

Warning

If this registry value is changed, the DHCP service will need to be restarted for the change to take effect.

## [Installing the NAC Windows Services](/docs/manac/nac-v8.1.1/configuration/dhcp-syslog-service-installation-and-configuration#installing-the-nac-windows-services)

The DHCP Syslog Service should be installed on all Windows DHCP servers used by any machine that will be managed by NAC. The installer install and starts a service on each DHCP server. No reboot of the server is required. If a mistake is made with one of the parameters, or if something changes at a later date, re-running the installer is completely safe.

## [Download the Installer to each domain controller](/docs/manac/nac-v8.1.1/configuration/dhcp-syslog-service-installation-and-configuration#download-the-installer-to-each-domain-controller)

The Windows services installer can be downloaded from:

<https://portal.myweblogon.com:8443/downloads/Tools/OPSWATServicesSetup.exe>

Info

If downloading from a network segment that is not managed by NAC, the internal IP address of the appliance (Manager node in a cluster) should be used in place of [p](http://auth.impulse.com)[ortal.myweblogon.com](http://portal.myweblogon.com).

## [Launching the Installer](/docs/manac/nac-v8.1.1/configuration/dhcp-syslog-service-installation-and-configuration#launching-the-installer)

Once the Installer is downloaded, double-click to run. Choose “Next” on the first screen.

Select the DHCPsyslog Service to install and click “Finish”. This will launch the next portion of the install.

If pre-requisites are not completed, a warning messages will be displayed and the installer will abort. If the message is displayed, please review for the pre-requisite section of this document.

## [Completing the DHCP Syslog Service Install](/docs/manac/nac-v8.1.1/configuration/dhcp-syslog-service-installation-and-configuration#completing-the-dhcp-syslog-service-install)

Click “Next” on the DHCP Syslog Service portion of the installer.

Under Enforcer IP, enter the internal IP address of the NAC appliance. In a cluster, this will be the Manager node. Click “Next”.

Choose the install location for the service. In most cases, the defaults will be sufficient. Click “Next”.

Click “Next” when prompted to create a Start Menu shortcut.

Click “Install” when ready.

Click “Finish” to close the installer.

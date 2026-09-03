<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration -->

# AD Connector Installation and Configuration

## [Necessary Pages](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#necessary-pages)

The information from these pages and URLs will be referenced in the steps below to complete AD Connector Installation and Configuration.

- [AD Connector Troubleshooting](https://docs.opswat.com/manac/knowledge-base/how-do-i-troubleshoot-adconnector-issues)
- <http://www.microsoft.com/en-us/download/details.aspx?id=21895>
- <https://portal.myweblogon.com:8443/downloads/Tools/OPSWATServicesSetup.exe>*
- <https://portal.myweblogon.com:8443/manage>*
- [Firewall](/docs/manac/nac-v8.1.1/operating/firewall)
- <https://portal.myweblogon.com:8443/manage/#/policy>*

Info

*In the links above, "[portal.myweblogon.com](http://portal.myweblogon.com)" can be replaced with the IP address of the NAC appliance or the custom hostname of the appliance, if applicable.

## [Troubleshooting](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#troubleshooting)

For troubleshooting related to AD Connector installation and configuration, see [AD Connector Troubleshooting](https://docs.opswat.com/manac/knowledge-base/how-do-i-troubleshoot-adconnector-issues).

## [AD Connector Prerequisites](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#ad-connector-prerequisites)

The following prerequisites will need to be completed on all domain controllers used by domain member machines being managed by NAC.

## [Configure Individual Domain Controllers to Audit Logon Events](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#configure-individual-domain-controllers-to-audit-logon-events)

On all Windows 2000+ domain controllers, open Local Security Policy under Administrative Tools.

Start Menu

Drill down to "Local Policy > Audit Policies".

Right click Audit Logon Events and select Properties.

Local Security Policy

Configure auditing of successful events as shown below. If the check boxes are grayed out, the active directory group policy that is being applied will need to be modified.

Audit Logon Events Properties

## [Configure All Domain Controllers to Audit Logon Events](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#configure-all-domain-controllers-to-audit-logon-events)

Access the Group Policy Management Console from Administrative Tools. For Windows 2000/2003 it can be [downloaded](http://www.microsoft.com/en-us/download/details.aspx?id=21895) or accessed from Group Policies from Active Directory Users and Computers.

Start menu

Right Click the Default Domain Controller Policy and select edit.

Group Policy Management

Drill down to "Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Audit Policy".

Right click Audit Logon Events and select Properties.

Group Policy Management Editor

Configure auditing of successful events as shown below.

Audit Logon Events Properties

## [Installing the Impulse Windows Services](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#installing-the-impulse-windows-services)

The AD Connector service should be installed on all domain controllers used by domain member machines that are managed by NAC. The installer installs and starts a service on each domain controller. No reboot of the server is required. If a mistake is made with one of the parameters, or if something changes at a later date, re-running the installer is completely safe.

### [Download the Installer to each domain controller](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#download-the-installer-to-each-domain-controller)

The Windows services installer can be downloaded from:

<https://portal.myweblogon.com:8443/downloads/Tools/OPSWATServicesSetup.exe>

Info

If downloading from a network segment that is not managed by NAC, the internal IP address if the appliance (Manager node in a cluster) should be used in place of [portal.myweblogon.com](http://auth.impulse.com).

## [Launching the Installer](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#launching-the-installer)

Once the Installer is downloaded, double-click to run. Choose “Next” on the first screen.

Welcome to the Impulse Services Installer Setup Wizard

Select the Services to install and click “Finish”. This will launch the next portion of the install. Note that the DHCPSyslog Service can be downloaded with the AD Connector or the AD Connector can be downloaded on its own by checking/unchecking the corresponding boxes.

Impulse Services Installer: Completing the Impulse Services Installer Setup Wizard

If pre-requisites are not completed, one of the following warning messages will be displayed and the installer will abort. If the following message is displayed, please review the pre-requisite section of this document.

Active Directory Not Installed

### [Completing the AD Connector Install](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#completing-the-ad-connector-install)

Click “Next” on the AD Connector portion of the installer.

Welcome to the AD Connector Setup Wizard

Under Policy Manager IP Address, enter the internal IP address of the NAC appliance. In a cluster, this will be the Manager node. The username and password should be a user with API read/write access. A user with API access should be created in the NAC configuration page <https://portal.myweblogon.com:8443/manage> Click “Next” when everything is entered.

AD Connector Setup: Configuration Information

Click “Next” to install in the default location.

AD Connector Setup: Select Destination Location

Review the parameters and click “Install” when ready.

AD Connector Setup: Ready to Install

Click “Finish” to complete the installer.

AD Connector Setup: Completing the AD Connector Setup Wizard

## [Firewall (Version 6.5.16 and Later)](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#firewall-version-6516-and-later)

To permit the AD Connector to talk to the NAC appliance:

1. Navigate to the Firewall UI from the Active Director Single Sign-On page by clicking "AD Connector Firewall Settings". Alternatively, navigate to [https://portal.myweblogon.com:8443/manage/#/configuration/firewall:8443/manage/#/configuration/firewall](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4084653_1_image2018-10-30_11-13-57.png) . “ [portal.myweblogon.com](http://portal.myweblogon.com) ” can be replaced with the IP address of the NAC appliance or the custom hostname of the appliance, if applicable.
2. Add the IP of each AD Server you have installed the AD Connector on to the list of approved source IPs on the AD Connector Access tab.

## [Policy Group Creation Using an AD device attribute](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#policy-group-creation-using-an-ad-device-attribute)

## [Setting up the device attribute qualifier for the domain attribute](/docs/manac/nac-v8.1.1/configuration/ad-connector-installation-and-configuration#setting-up-the-device-attribute-qualifier-for-the-domain-attribute)

Navigate to the Policy Manager: [https://portal.myweblogon.com:8443/manage/#/policy](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4084653_1_image2018-10-30_11-13-57.png). If accessing the appliance from a network segment that is not managed by NAC , the inside IP address of the appliance should be used in place of " portal.myweblogon.com ". In a cluster, this will be the manager node. Once the Management Console is open, navigate to "Policy Manager > Qualifiers Menu > Device Attributes". Click the “New” button on the bottom right and enter a name. Since the device attribute will be coming from Active Directory, choose “ActiveDirectory” as the Device Attribute Source. “Domain” is the only option for the Device attribute name. The last step is the enter the value under “Device Attribute Value”. NAC will only use the values that have been configured. When finished, click “Save”.

The qualifier is now ready to be added to a qualifier set and subsequently added to a qualifier container followed by a Policy Group.

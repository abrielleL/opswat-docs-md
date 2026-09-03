<!-- source: https://www.opswat.com/docs/manac/configuration/windows-services-setup-guide -->

# Windows Services Setup Guide

ADConnector is used to enable Single Sign-On capability between the NAC and domain domain devices (both Windows and Macintosh) without the need for a Policy Key or RADIUS accounting. This means users who have logging into their machines with domain credentials will not need to enter the same credentials again at a captive portal prompt. If your switches/WLCs are already configured to send RADIUS accounting to the NAC, or if the devices for which you would like AD SSO functionality enabled already have the Policy Key installed, you should not need to install ADConnector.

The DHCP Syslog service publishes logging from your Windows DHCP server to the NAC. This provides IP address to MAC address correlation, enabling device details to be persisted across multiple sessions. RADIUS accounting generally provides equivalent correlation data, so if your switches/WLCs are already configured to send RADIUS accounting to the NAC, you should not need to install the DHCP Syslog service.

The OPSWAT AD Connector has been introduced to collect all AD Sign-on events from one or more Active Directory Services (supports Windows Server 2003 and Windows Server 2008, and Server 2012). The sign on events will be sent from the Active Directory Servers to the NAC Policy Manager for Single Sign-On and Device Ownership assignment.

As of the 6.0.1 release of NAC, domain member Windows and Macintosh machines no longer require a policy key to use domain style single sign-on. This release also adds the device attribute feature. Domain machines can now be place into Policy Groups based on attributes defined for the device in Active Directory.

## [How NAC leverages DHCP information](/docs/manac/configuration/windows-services-setup-guide#how-nac-leverages-dhcp-information)

**Device Persistence:** DHCP data provides the necessary mac address information to allow NAC to track a single device after multiple IP lease expiration. The result is that users have the ability to more easily use their devices after leaving the network and returning later.

**Policy Enforcement by Mac Address:** With DHCP information, enforcement for non-Policy Key devices can be applied based on a mac address. In most environments, a mac address is much more reliable since IP assignments change over time.

**Device Enrollment:** NAC provides the ability to enroll network-enabled media and gaming devices. Before this functionality can work, NAC must have a reliable source, such as DHCP, for obtaining mac address information for these devices.

The Purpose of this document is to outline the steps required to configure an Active Directory environment to Single Sign-On domain member Windows and Macintosh machines to a NAC system and send device specific attributes to NAC and to configure a Windows DHCP server to forward DHCP syslog to a NAC environment.

##

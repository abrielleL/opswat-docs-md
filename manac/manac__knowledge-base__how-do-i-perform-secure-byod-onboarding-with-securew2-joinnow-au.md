<!-- source: https://www.opswat.com/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au -->

# How do I perform Secure BYOD onboarding with SecureW2 JoinNow/AutoConnect?

## [JoinNow - Onboarding Client](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#joinnow---onboarding-client)

### [What is JoinNow?](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#what-is-joinnow)

JoinNow is the tool that actually does the autoconfiguration of the endpoint. JoinNow is the portion that we have rebranded as AutoConnect.

### [What OSes are supported by SecureW2?](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#what-oses-are-supported-by-securew2)

SecureW2 supports all the major players.

### [What remediation Resources need to be allowed by SecureW2?](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#what-remediation-resources-need-to-be-allowed-by-securew2)

At a minimum, both SecureW2 IPs must be allowed. Adding access to Google Play is not required but is highly recommended.

### [What information is needed to configure a SecureW2 provisioning profile?](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#what-information-is-needed-to-configure-a-securew2-provisioning-profile)

A questionnaire can be sent with the information that will be needed to set up a profile by contacting Customer Success at [opswat.com/support](https://www.opswat.com/support/)

### [Is the onboarding SSID really needed?](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#is-the-onboarding-ssid-really-needed)

If a device is onboarding using SecureW2, any SSIDs the user starts on is important to have in the configuration. The reason for this is that SecureW2 cannot set SSID precedence on an SSID it does not know about. If SecureW2 is run from an SSID that is not specified the whole process may appear to be broken since nothing is being done to the open/onboarding SSID on the device and there is a very high chance the device might connect back to that SSID instead of the Secure SSID.

### [Devices keep getting "Network Out of Range" errors but connect just fine afterward when manually choosing the secure SSID.](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#devices-keep-getting-network-out-of-range-errors-but-connect-just-fine-afterward-when-manually-choosing-the-secure-ssid)

This is usually caused by one or more of these items and the JoinNow client timing out:

- The device is trying to connect to another remembered SSID that is not accounted for in the JoinNow client.
- The device is a domain machine and has a wireless SSID profile pushed out through group policy.
- A Delay in acquiring an IP address.
- A Delay in the key exchanges.

Steps to resolve:

- Ensure that all remembered SSIDs are removed from the device or set to be removed by the JoinNow client. If the device connects to a different SSID, this is likely the issue.
- If the first step doesn't resolve the issue, check again to be sure.
- If the device is a domain machine and has an SSID profile pushed out through group policy, ensure that the device is NOT connected to that SSID. JoinNow is not intended for these devices, and performance may be impacted.
- If remembered SSIDs aren't the issue, the performance of the RADIUS server and/or DHCP server may be the cause. In an RBE environment, the disconnect delay may need to be increased a second or two.

### [After a device has been onboarded, how do you reset the device?](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#after-a-device-has-been-onboarded-how-do-you-reset-the-device)

- Windows - Forget the SSID
- Android - Forget the SSID (optionally uninstall the SecureW2 JoinNow App)
- iOS (iPhone/iPad) - Remove the Profile: **Settings** > **General** > **Profiles** - Delete the profiles
- Mac OS - Forget the SSID and Remove Profile: **System Settings** > **Profiles**

## [CA Connector](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#ca-connector)

### [What is SW2 CA Connector?](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#what-is-sw2-ca-connector)

SecureW2 Certificate Authority plugin designed to simplify client certificate provisioning process. NOTE: All support requests must be submitted to [support@securew2.com](mailto:support@securew2.com)

### [What are the deployment Scenarios?](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#what-are-the-deployment-scenarios)

Standalone Active Directory is used to set up a Connector on a single VM instance in the Customer environment. Users can be authenticated using the Customer backend; however, the ADCS is set up in a separate environment.

Integration with existing Active Directory. Connector and ADCS Integration Service run on separate Domain servers. A Secure and Encrypted channel is established between the Connector and the ADCS Integration service to ensure maximum security.

Integration with Symantec MPKI

### [What are the System Requirements?](/docs/manac/knowledge-base/how-do-i-perform-secure-byod-onboarding-with-securew2-joinnow-au#what-are-the-system-requirements)

Hardware configuration

1. Windows Server 2008 R2, 2012 R2 (Standard or Datacenter edition)
2. Minimum (HW/VM) - CPU: 2GHz Single processor Memory: 4GB
3. Disk: 60GB
Service configuration on the Windows Server

1. Windows 2008 R2, 2012 R2 with a standalone/separate AD domain
2. IIS Role.
3. Enterprise ADCS (NOT standalone) Role.
4. We need user account member of domain admin and Enterprise admin group. Windows 2008 R2, 2012 R2 with a standalone/separate AD domain
5. SSL web server certificate from any public CA ( This web server certificate will be configured for JoinNow Connector service) So that the connection/communication between the end device and the JoinNow connector will be secured using TLS.
Firewall Requirements on the Certificate Server

1. Inbound port 443 - In order to help improve the end-user experience, this is recommended to be open to the whole internet. Cloud management of certificates also requires this.
2. Must be able to connect to the Domain controller for authentication over LDAP/389 or LDAPS/636.
3. Must be able to connect to the Domain controller using Kerberos on port 464.
4. DCOM/RPC needs port TCP/135 and one additional Random port.
5. See also: <http://blogs.technet.com/b/pki/archive/2010/06/25/firewall-roles-for-active-directory-certificate-services.aspx>
6. See also: <https://support.microsoft.com/en-us/kb/832017>

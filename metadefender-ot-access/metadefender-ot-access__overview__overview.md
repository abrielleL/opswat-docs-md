<!-- source: https://www.opswat.com/docs/metadefender-ot-access/overview/overview -->

# Introduction

MetaDefender OT Access™ is a remote access tool that provides a platform for facilitating and monitoring connections between remote users and industrial assets. The software contains built-in tools for security and manageability.

MetaDefender OT Access features include:

- The ability to deploy in the Cloud or onsite
- The Cloud deployment has no required hardware and can be set up in one day or less.
- The onsite Management Console is easy to install. This deployment can also be set up in one day.
- Integrates with your Active Directory server for user and Security Group authorization
- Enables Policy Enforcement per user and per session
- Outbound-only connection from endpoint gateway to MetaDefender OT Access cloud or on-prem instance, with no inbound firewall exceptions required
- Inexpensive and flexible pricing model on annual or monthly subscription
- Cloud components are hosted on Amazon Web Services (AWS) for maximum reliability and performance

#### [MetaDefender OT Access deployments](/docs/metadefender-ot-access/overview/overview#metadefender-ot-access-deployments)

MetaDefender OT Access has two possible deployments:

- Cloud: OPSWAT manages some aspects of MetaDefender OT Access configuration, including uploading performing software updates at the customers request, and setting Management IPs.
- Onsite: The customer manages all MetaDefender OT Access configuration tasks. All traffic inspection and policy enforcement are performed in the onsite server, making it suitable for offline deployments with no internet access.

Except for the Management Console, both deployments have the same functionality. You will receive the equipment, software, etc. appropriate to your deployment.

#### [Supported protocols](/docs/metadefender-ot-access/overview/overview#supported-protocols)

Both MetaDefender OT Access deployments support various IT and OT protocols. Refer to Appendix 1 for a table of protocols and their associated policies.

#### [IT protocols](/docs/metadefender-ot-access/overview/overview#it-protocols)

The following IT protocols support both client-based and client-less access:

- RDP
- SSH
- VNC
- Telnet
- HTTPS

The following IT protocols support client-based access only:

- HTTP
- Generic TCP

#### [OT protocols](/docs/metadefender-ot-access/overview/overview#ot-protocols)

OT protocols support client-based access only:

- EtherNet/IP
- FINS
- MODBUS
- OPCUA
- S7Comm
- SLMP

#### [MetaDefender OT Access components](/docs/metadefender-ot-access/overview/overview#metadefender-ot-access-components)

MetaDefender OT Access components differ, depending on the deployment:

- **System Configuration Console (on-prem only):** Used to perform internal configuration tasks the MetaDefender OT Access instance, such as license activation and static IP configuration. Refer to the *Management Console Guide* for more information.
- **Management Console (on-prem or cloud):** Used to for everyday manage tasks such as provisioning users, configuring services, and monitoring connections between remote users the OT assets / services to which they have been granted access.
- **Windows Client / MetaDefender Endpoint:** Connects the remote user's computer to the cloud or on-prem MetaDefender OT Access instance, and ultimately to their OT assets.
- **Windows Service Client:** Windows system-level service that can be used as an alternative to the Windows Client. The service launches automatically when the system boots.

#### [Appendix 1: Protocols and Policies](/docs/metadefender-ot-access/overview/overview#appendix-1-protocols-and-policies)

| **Protocol** | **Policy** | **Description** |
| --- | --- | --- |
| Ethernet IP | None | N/A |
| FINS | Read Only | Read:   - Broadcast test result - Clock - Controller data mode - Controller data status - Cycle time - Data link status - Data link table - Errors log - FAL/FALS messages - File parameters and content of files stored in the device - Memory areas - Network status - Parameter area - Program area |
| FINS | Full Access | Unrestricted access |
| HTTP | Full Access | Protect against SQL injection and cross-site scripting |
| HTTPS | None | N/A |
| Modbus | Read Only | Read registers or coils |
| Modbus | Standard_Ops | Allow the following Modbus operation codes:   - 1 - 2 - 3 - 4 - 5 - 6 - 7 - 8 - 11 - 12 - 15 - 16 - 17 - 20 - 21 - 22 - 23 - 24 - 43 |
| Modbus | Full Access | Unrestricted access |
| OPCUA | Read Only | Deny the following OPCUA operation codes:   - 670 - 673 - 679 - 751 - 763 - 769 - 775 - 781 - 787 - 793 - 799 - 826 - 832 - 841 - 847 |
| OPCUA | All Access | Unrestricted access |
| RDP | None | N/A |
| S7COMM | Read Only | Read   - Alarm query - CPU states - Clock - Diagnostic information - Variables Download - Get the program that was loaded in the PLC |
| S7COMM | Full Access | Unrestricted access |
| SLMP | Read Only | Read:   - Data of CPU module devices - Data of SLMP-compatible devices - Data using labels - Memory buffer of intelligent function module - Parameters and programs from CPU module and SLMP compatible devices |
| SLMP | Full Access | Unrestricted access |
| SSH | None | N/A |
| Telnet | None | N/A |
| VNC | None | N/A |

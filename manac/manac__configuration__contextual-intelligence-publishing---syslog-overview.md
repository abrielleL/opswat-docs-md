<!-- source: https://www.opswat.com/docs/manac/configuration/contextual-intelligence-publishing---syslog-overview -->

# Contextual Intelligence Publishing - Syslog Overview

## [Overview](/docs/manac/configuration/contextual-intelligence-publishing---syslog-overview#overview)

Contextual Intelligence Publisher can be configured to export syslog data in CEF, LEEF and Key-Value formats. The syslog data will help to correlate data in a syslog collector with device data from NAC.

## [Configure the Syslog collector](/docs/manac/configuration/contextual-intelligence-publishing---syslog-overview#configure-the-syslog-collector)

On the Syslog collector system, configure the NAC Policy Manager IP as a valid source of Syslog.

## [Configure CIP](/docs/manac/configuration/contextual-intelligence-publishing---syslog-overview#configure-cip)

Once the Syslog Collector has been configured, navigate to the NAC Configuration at <https://portal.myweblogon.com:8443/manage> ([portal.myweblogon.com](http://portal.myweblogon.com/) can be replaced by the manager IP or a branded URL) and choose “Contextual Intelligence.” Click on “Add” and enter the following information:

- **Publisher:** Syslog
- **Name:** A name to describe where CIP is publishing Data.
- **Host:** IP address of the Syslog Collector
- **Port**: listen port of the Syslog Collector
- **Facility**: Can be set to whatever is preferred in the Syslog Collector
- **Level**: Can be set to whatever is preferred in the Syslog Collector
- **Format:** The format best suited for you Syslog Collector

Once finished, click “Submit” and continue to the next section to verify the integration.

## [Syslog Sample Outputs](/docs/manac/configuration/contextual-intelligence-publishing---syslog-overview#syslog-sample-outputs)

### [Key-Value Format (Splunk Compatible):](/docs/manac/configuration/contextual-intelligence-publishing---syslog-overview#key-value-format-splunk-compatible)

Dec 30 15:46:42 syslog1: clientId="4", currentIp="10.101.111.15", localIP="null",
macAddress="005056ae4b8e", machineName="null", hostRefType="PC", policyGroup="My Group",
deviceAttributes="LDAP:UserDomain:PD", username="tester1", roles="TestUsers", complianceState="compliant",
failedPolicy="null", eventType="authentication"
### [LEEF Format (QRadar compatible, tab delimited):](/docs/manac/configuration/contextual-intelligence-publishing---syslog-overview#leef-format-qradar-compatible-tab-delimited)

Dec 30 15:46:42 syslog3: LEEF:1.0|OPSWAT|IdentityPublisher|1.0.5|clientDelta|clientId=4
src=10.101.111.15 localIp=null srcMAC=005056ae4b8e machineName=null hostRefType=PC policyGroup=My Group
deviceAttributes=LDAP:UserDomain:PD usrName=tester1 role=TestUsers complianceState=compliant
failedPolicy=null evenType=login
### [CEF Format (ArcSight compatible, space delimited):](/docs/manac/configuration/contextual-intelligence-publishing---syslog-overview#cef-format-arcsight-compatible-space-delimited)

Dec 30 15:46:42 syslog2: CEF:0|OPSWAT|IdentityPublisher|1.0.5|clientDelta|clientDelta|1|suid=4
src=10.101.111.15 cs1Label=localIP cs1=null smac=005056ae4b8e cs2Label=machineName cs2=null
cs3Label=hostRefType cs3=PC cs4Label=policyGroup cs4=My Group cs5Label=deviceAttributes
cs5=LDAP:UserDomain:PD suser=tester1 cs6Label=roles cs6=TestUsers cs9Label=complianceState cs9=compliant
cs10Label=failedPolicy cs10=null cs11Label=eventTyle cs11=logout
## [Field Definitions and Descriptions](/docs/manac/configuration/contextual-intelligence-publishing---syslog-overview#field-definitions-and-descriptions)

| Key-Value | LEEF | CEF | Description |
| --- | --- | --- | --- |
| clientId | clientId | suid | The id of the client record in the NAC database |
| currentIp | src | src | The IP address of this client. This is the IP address of the device as seen from the network. |
| localIp | localIp | localIp | The IP address of this client as reported by the NAC policy key, if it is installed. This may differ from the ‘currentIp’ if the client is behind a NAT device. |
| macAddress | srcMAC | smac | The MAC address of the client |
| machineName | machineName | machineName | The machine name of the client |
| hostRefType | hostRefType | hostRefType | One of a list of strings describing the type of device. Values can be one of:   - Android - Apple Mobile - BlackBerry - ChromeOS - iPad - Linux - MAC - Media - Microsoft Gaming Device - Miscellaneous - Nintendo Gaming Device - Nokia Mobile - Palm - PC - Sony Gaming Device - Windows Mobile - VoIP Phone |
| policyGroup | policyGroup | policyGroup | The name of the policy group this client belongs to, as configured in the NAC policy manager |
| deviceAttributes |  |  | An array of strings that represent any device attributes associated with the client. A device attribute is represented in the string as “SOURCE:NAME:VALUE”. (EX: a client with a device attribute from ‘ActiveDirectory’ with name ‘Domain’ and value ‘opswat’ would be represented as “ActiveDirectory:Domain:opswat”. |
| username | usrName | suser | The username this client is authenticated with. This is identical to the first entry in the ‘principal’ field. |
| roles | role | roles | Each entry is a string role name, identical to the roles reported following the username in the ‘principal’ field |
| complianceState | complianceState | complianceState | Will be either ‘compliant’ or ‘not compliant’ |
| failedPolicy | failedPolicy | failedPolicy | Contains the name of a policy that is causing the device to be ‘not compliant’ |
| eventType | eventType | eventType | The type of event that caused the packet to be sent:   - Login - Logout - Authentication - complianceChange |

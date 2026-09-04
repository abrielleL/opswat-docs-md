<!-- source: https://www.opswat.com/docs/manac/configuration/contextual-intelligence-publisher-outputs -->

# Contextual Intelligence Publisher Outputs

Each publisher type available in the Contextual Intelligence module is capable of publishing a subset of the data provided by NAC, as dictated by the available APIs for the vendor in question.

## [Master List](/docs/manac/configuration/contextual-intelligence-publisher-outputs#master-list)

The list of data points provided by NAC:

- Client ID
- Principal

  - This is the full principal, complete with username and roles
  - Some publishers may provide only the username from this, others username and role
- IP Address
- MAC Address
- Machine Name
- Host Type
- Policy Group
- Domain
- Compliance State

## [iboss Publisher](/docs/manac/configuration/contextual-intelligence-publisher-outputs#iboss-publisher)

- Username
- IP Address
- MAC Address
- Group Memberships (LDAP roles AND NAC roles)
- Machine Name
- Domain

Sample Data:

http://10.0.5.35:8015/nacAgent?action=logon&user=adam.parker&dc=SafeConnect&key=XS832CF2A&ip=10.30.0.234&g=Users,Iboss+-+Full+Access,MIS,Technology,Group+Management+Admin
## [Juniper SRX (Requires 6.3+)](/docs/manac/configuration/contextual-intelligence-publisher-outputs#juniper-srx-requires-63)

- Username
- IP Address
- Group Memberships (LDAP roles AND NAC roles)
- Device Type
- Machine Name
- Compliance State

Sample Data:

<userfw-entries>
<userfw-entry>
<source>Aruba ClearPass</source>
<timestamp>2017-03-20T18:37:50Z</timestamp>
<operation>logon</operation>
<IP>192.168.2.101</IP>
<domain/>
<user>testuser</user>
<role-list>
<role>Guest</role>
</role-list>
<posture>Healthy</posture>
<device_category>Computer</device_category>
<device_family>Windows</device_family>
<device_name/>
</userfw-entry>
## [Palo Alto Publisher](/docs/manac/configuration/contextual-intelligence-publisher-outputs#palo-alto-publisher)

- Username
- IP Address
- Domain
- Device Type
- Machine Name

Sample Data:

<uid-message>
<version>1.0</version>
<type>update</type>
<payload>
<login>
<entry ip="1.1.1.1" name="Domain\Username">
<hip-report>
<md5-sum>MD5SUM</md5-sum>
<user-name>Username</user-name>
<host-name>Username</host-name>
<domain>domain-Test</domain>
<ip-address>1.1.1.1</ip-address>
<categories>
<entry name="host-info">
<client-version>Apple Mobile</client-version>
</entry>
</categories>
</hip-report>
</entry>
</login>
</payload>
</uid-message>
## [Exinda Publisher](/docs/manac/configuration/contextual-intelligence-publisher-outputs#exinda-publisher)

- Username
- IP Address
- Domain
- Group Memberships (LDAP roles AND NAC roles)

Sample Data:

<login>
<user>MYDOMAIN\email@opswat.com</user>
<ip-addr>10.101.111.15</ip-addr>
<time>0</time>
</login>
<user>
<name>MYDOMAIN\email@opswat.com</name>
<group>Users</group>
<group>Auth</group>
<group>SC_NonCompliant</group>
</user>
## [Procera Publisher](/docs/manac/configuration/contextual-intelligence-publisher-outputs#procera-publisher)

- Device Current IP Address
- Device Local IP Address (If a policy key is installed)
- Username
- Group Memberships (LDAP roles AND NAC roles)
- Device Mac Address
- Machine Name (if available)
- Device Type
- Policy Group
- Domain

Sample Data:

{
"id": 1,
"clientId": 1,
"currentIp": "10.101.33.10",
"localIp": "10.101.33.10",
"macAddress": "aabbccddeeff",
"machineName": "travis-dev",
"principal": "developer,administrator",
"hostRefType": "PC",
"policyGroup": "testGroup",
"username": "username",
"roles": "developer,administrator",
"deviceAttributes": "Active-Directory:Domain:PD,MDM:Ownership:Personally Liable"
}
## [JSON Publisher](/docs/manac/configuration/contextual-intelligence-publisher-outputs#json-publisher)

- Client ID
- Principal
- IP Address
- MAC Address
- Machine Name
- Host Type
- Policy Group
- Domain

Sample Data:

{
"title":"Client",
"description":"A SafeConnect client",
"type":"object",
"properties":{
"clientId":{
"type":"integer"
},
"currentIp":{
"type":"string"
},
"localIp":{
"type":"string"
},
"macAddress":{
"type":"string"
},
"machineName":{
"type":"string"
},
"principal":{
"type":"string"
},
"hostRefType":{
"type":"string"
},
"policyGroup":{
"type":"string"
},
"username":{
"type":"string"
},
"roles":{
"type":"array",
"items":{
"type":"string"
},
"minItems":0,
"uniqueItems":true
},
"deviceAttributes":{
"type":"array",
"items":{
"type":"string"
},
"minItems":0,
"uniqueItems":true
}
}
}
## [RADIUS Accounting](/docs/manac/configuration/contextual-intelligence-publisher-outputs#radius-accounting)

Note that this does not require any flavor or pre-existing RADIUS or RBE. This is simply CIP repacking Contextual Intelligence data as RADIUS accounting.

- Device IP Address
- Device Mac Address
- Username
- Login Time (RADIUS Start)
- Logout Time (RADIUS Stop)
- NOTE: We do not currently send Interim-Updates. Because of this, ensure that the receiving end has session/idle timeouts set to the maximum value.
- Vendors that we know support RADIUS accounting as an input:

  - Fortinet (Requires the FortiAuthenticator Module)
  - SonicWALL
  - Lightspeed
  - WatchGuard Firebox Firewall - <http://www.watchguard.com/help/docs/fireware/11/en-US/Content/en-US/authentication/rsso_enable.html>

## [Syslog Publisher](/docs/manac/configuration/contextual-intelligence-publisher-outputs#syslog-publisher)

Fields (All syslog formats publish the following fields):

- Client ID
- Username
- Roles
- Current IP Address
- Local IP Address
- MAC Address
- Machine Name
- Host Type
- Policy Group
- Device Attributes

## [Key-Value Format (Splunk compatible)](/docs/manac/configuration/contextual-intelligence-publisher-outputs#key-value-format-splunk-compatible)

Dec 30 15:46:42 syslog1: clientId="4", currentIp="10.101.111.15", localIP="null", macAddress="005056ae4b8e", machineName="null", hostRefType="PC", policyGroup="My Group", deviceAttributes="LDAP:UserDomain:PD", username="tester1", roles="TestUsers", complianceState="compliant", failedPolicy="null", eventType="authentication"
## [LEEF Format (Qradar compatible, tab delimited)](/docs/manac/configuration/contextual-intelligence-publisher-outputs#leef-format-qradar-compatible-tab-delimited)

Dec 30 15:46:42 syslog3: LEEF:1.0|OPSWAT|IdentityPublisher|1.0.5|clientDelta|clientId=4 src=10.101.111.15 localIp=null srcMAC=005056ae4b8e machineName=null hostRefType=PC policyGroup=My Group deviceAttributes=LDAP:UserDomain:PD usrName=tester1 role=TestUsers complianceState=compliant failedPolicy=null eventType=authentication
## [CEF Format (ArcSight compatible, space delimited)](/docs/manac/configuration/contextual-intelligence-publisher-outputs#cef-format-arcsight-compatible-space-delimited)

Dec 30 15:46:42 syslog2: CEF:0|OPSWAT|IdentityPublisher|1.0.5|clientDelta|clientDelta|1|suid=4 src=10.101.111.15 cs1Label=localIP cs1=null smac=005056ae4b8e cs2Label=machineName cs2=null cs3Label=hostRefType cs3=PC cs4Label=policyGroup cs4=My Group cs5Label=deviceAttributes cs5=LDAP:UserDomain:PD suser=tester1 cs6Label=roles cs6=TestUsers cs9Label=complianceState cs9=compliant cs10Label=failedPolicy cs10=null cs11Label=eventType cs11=authentication
## [Field Definitions and Descriptions](/docs/manac/configuration/contextual-intelligence-publisher-outputs#field-definitions-and-descriptions)

| Key-Value | LEEF | CEF | Description |
| --- | --- | --- | --- |
| **clientId** | **clientId** | **clientId** | The id of the client record in the NAC database. |
| **currentIp** | **src** | **src** | The IP address of this client. This is the IP address of the device as seen from the network. |
| **localIp** | **localIp** | **localIp** | The IP address of this client as reported by the NAC policy key, if it is installed. This may differ from the ‘currentIp’ if the client is behind a NAT device. |
| **macAddress** | **srcMAC** | **smac** | The MAC address of the client |
| **machineName** | **machineName** | **machineName** | The machine name of the client |
| **hostRefType** | **hostRefType** | **hostRefType** | One of a list of strings describing the type of device. Values can be one of:   - Android - Apple Mobile - BlackBerry - iPad - Linux - MAC - Media - Microsoft Gaming Device - Miscellaneous - Nintendo Gaming Device - Nokia Mobile - Palm - PC - Sony Gaming Device - Windows Mobile |
| **policyGroup** | **policyGroup** | **policyGroup** | The name of the policy group this client belongs to, as configured in the NAC policy manager |
| **deviceAttributes** |  |  | An array of strings that represent any device attributes associated with the client. A device attribute is represented in the string as “SOURCE:NAME:VALUE”. (EX: a client with a device attribute from ‘ActiveDirectory’ with name ‘Domain’ and value ‘OPSWAT’ would be represented as “ActiveDirectory:Domain:opswat”. |
| **username** | **usrName** | **suser** | The username this client is authenticated with. This is identical to the first entry in the ‘principal’ field. |
| **roles** | **role** | **roles** | Each entry is a string role name, identical to the roles reported following the username in the ‘principal’ field |
| **complianceState** | **complianceState** | **complianceState** | Will be either ‘compliant’ or ‘not compliant’ |
| **failedPolicy** | **failedPolicy** | **failedPolicy** | Contains the name of a policy that is causing the device to be ‘not compliant’ |
| **eventType** | **evenType** | **eventType** | The type of event that caused the packet to be sent:   - Session Start - Session Stop - Authentication |

## [IF-MAP Publisher](/docs/manac/configuration/contextual-intelligence-publisher-outputs#if-map-publisher)

- Username
- IP Address
- MAC Address

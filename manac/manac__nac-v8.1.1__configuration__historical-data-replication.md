<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/historical-data-replication -->

# Historical Data Replication

Setting up the connection between the NAC appliance(s) and historical backup database.

## [Step-by-step guide](/docs/manac/nac-v8.1.1/configuration/historical-data-replication#step-by-step-guide)

1. Identify a target machine with MySQL 5.5.x to 5.7.x installed. Alternatively, MariaDB 5.5.x to 5.7.x may also be used.
2. Make sure all NAC Appliances have a clear logical route to this machine on port 3306.
3. Create the database.
4. Grant the NAC Appliance privileges to this database.

Info

Assuming your database is named “backupDB”, the MySQL commands would look like the following. Please note that the 'USERNAME' and 'PASSWORD' fields can be whatever you want, as long as you preserve the single quotes.

use backupDB
grant all privileges on backupDB.* to 'USERNAME'@'%' identified by 'PASSWORD';
flush privileges;

Once the above is completed forward the database name, username and password to your Impulse Support representative, along with the target machine’s IP. Your representative will finish the setup and contact you for verification.

Note

The replication cycle is configurable, defaulting to every 5 minutes. It’s a good idea to thin the table periodically, as data volume can grow quite large over time. Storage size should be allocated at 1 GB per year, for every 1000 concurrent users. Due to a third party dependency, MySQL 5.6.x or greater is currently unsupported for this feature.

## [Setting up the Database Table](/docs/manac/nac-v8.1.1/configuration/historical-data-replication#setting-up-the-database-table)

You can use the following script to set up the Clienthist table in your target MySQL database.

CREATE TABLE clienthist ( clientHistId bigint(20) unsigned NOT NULL auto_increment, PRIMARY KEY (clientHistId), transType char(15) NOT NULL , transDate timestamp NOT NULL , -- client header info clientId bigint(20) unsigned NOT NULL default '0', sessionUID varchar(32) NOT NULL default '', currentIpAddress char(15) NULL , principal text, ugroupId mediumint(9) unsigned NULL, ugroupLabel varchar(255) , hostreftypeId mediumint(9) unsigned NOT NULL default '0', hostreftypeLabel varchar(255) NOT NULL default '', policyCompliance text, winMachineName varchar(85), macaddress varchar(25) , localIpAddress char(15) NULL , routerIpAddress char(15) NULL , webMessageId mediumint(9) unsigned NULL, webMessageLabel varchar(150) , webMessageViewName varchar(50) , osName varchar(25) NULL, -- client state outCompliancePolicyId mediumint(9) unsigned NOT NULL default '0', outCompliancePolicyLabel varchar(255) NULL, outComplianceadminMsgIds varchar(255) null, groupUpdated tinyint(1) NOT NULL default '0', quarantined tinyint(1) NOT NULL default '0', ilan tinyint(1) NOT NULL default '0' ) ENGINE=InnoDB;
## [Guide to the Fields](/docs/manac/nac-v8.1.1/configuration/historical-data-replication#guide-to-the-fields)

What follows is a high level breakdown of the fields in the clienthist table. Please contact your Impulse Point Support or Service Delivery Specialist for more details.

| Field | Description |
| --- | --- |
| clientHistId | Primary key for the clienthist table. Typically not used for troubleshooting or reporting. |
| transType | How NAC interacted with the endpoint. |
| transDate | Time at which this interaction occurred. |
| clientId | Primary key from the internal table that tracks an endpoint’s status while it’s online. Typically only used by Impulse Point personnel. |
| sessionUID | Unique identifier for a Policy Key device. Rotates with each active session. Will read “NEW” for non-Policy Key devices. |
| currentIpAddress | Endpoint’s IP address, as reported by the network. |
| principal | Combination of network authentication username, plus any applicable role information from AD, LDAP, or Safe•Connect device enrollment. Format: “USERNAME,ROLE1,ROLE2,ROLE3,etc.” |
| ugroupId | Identifies the endpoint’s NAC policy group. |
| ugroupLabel | NAC policy group name, as displayed in the Policy Manager. |
| hostreftypeId | Numerically represents NAC’s current assessment of an endpoint’s device type. |
| hostreftypeLabel | The common name associated with each hostreftypeId. |
| policyCompliance | Lists all policies applicable to a given endpoint, along with their compliance state. |
| winMachineName | Endpoint’s device name as received from DHCP or the Policy Key. |
| macaddress | Endpoint’s mac address as received from DHCP, Radius accounting, or the Policy Key. |
| localIpAddress | The IP address reported by the Policy Key. Will differ from the currentIpAddress 1) if the endpoint is downstream of a home router using NAT, or 2) temporarily, if the device is switching from wired to wireless, or vice versa. |
| routerIpAddress | IP address of the Layer 3 switch that forwarded the endpoint’s flow (eg, Netflow, Sflow, Aruba mirrored traffic) data to NAC. This is the device where enforcement will take place if the endpoint should be quarantined. A blank routerIpAddress indicates that 1) no relevant flow data has been received, and consequently 2) the device cannot be quarantined. |
| webMessageId | Identifies which enforcement message was displayed to the endpoint, if any. |
| webMessageLabel | Common name associated with the webMessageId. This is also how the message will be displayed in the Policy Manager’s Custom Messaging module, if applicable. |
| webMessageViewName | Enforcement message’s location on the enforcer’s file system. Typically useful for customers who have direct SSH access to edit the messaging. |
| osName | Reported by the Policy Key if applicable, a more detailed variant of the hostreftypeLabel. |
| outCompliancePolicyId | Identifies the topmost non-compliant policy in the endpoint’s policy tree. This is the policy for which the endpoint will receive any applicable messaging or enforcement actions. |
| outCompliancePolicyLabel | Common name associated with the outCompliancePolicyId. This is the policy name as displayed in the Policy Manager and Dashboard. |
| outComplianceadminMsgIds | Identifies supplementary messaging associated with a given policy. |
| groupUpdated | A value of “1” indicates that a Policy Manager upload has occurred since the last time the endpoint communicated with SafeConnect. |
| quarantined | A value of “1” indicates that the endpoint is due to be blocked at the Layer 3 switch for policy compliance. |
| ilan | A value of “1” indicates that the endpoint is due to be blocked using the Policy Key’s ILAN technology for policy compliance. |

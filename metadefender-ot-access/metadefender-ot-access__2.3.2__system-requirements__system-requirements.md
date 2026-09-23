<!-- source: https://www.opswat.com/docs/metadefender-ot-access/2.3.2/system-requirements/system-requirements -->

[MetaDefender OT Access](https://www.opswat.com/docs/metadefender-ot-access/overview)Need Help?
# System Requirements

## [MetaDefender OT Access On premise](/docs/metadefender-ot-access/2.3.2/system-requirements/system-requirements#metadefender-ot-access-on-premise)

Your server must meet the following requirements before installing MetaDefender Endpoint MetaDefender OT Access.

### [Minimum Hardware Requirement](/docs/metadefender-ot-access/2.3.2/system-requirements/system-requirements#hardware-sizing)

| RAM | 8 GB |
| --- | --- |
| CPU | 1 CPU (4 cores) |
| Hard disk | 60 GB |

### [Software Requirement](/docs/metadefender-ot-access/2.3.2/system-requirements/system-requirements#ports-used)

The server software includes the OS, installed from an ISO either onto a VM or bare metal (VM strongly recommended). Because of this, it has no external software requirements. The ISO includes all the software it needs

### [Hardware sizing](/docs/metadefender-ot-access/2.3.2/system-requirements/system-requirements#browser-requirement)

The following table provides recommendations on how to scale hardware specs for a MetaDefender OT Access on-premise deployment based on the number of concurrent connected devices needing to be serviced.

| Number of devices | 1,000 | 1,000 to 5,000 |
| --- | --- | --- |
| CPU | 1 CPU ( 4 cores) | 1 CPU ( 8 cores) |
| RAM | 8 GB | 16 GB |
| Hard disk capacity | 60 GB | 120 GB |

### [Ports used](/docs/metadefender-ot-access/2.3.2/system-requirements/system-requirements#metadefender-ot-access-gateway)

The table below shows the default port configuration of MetaDefender OT Access. The ports listed under **External** should be opened for external access.

| OPSWAT Product | Port |
| --- | --- |
| Management Console | 443 and 8443 |

### [Browser Requirement](/docs/metadefender-ot-access/2.3.2/system-requirements/system-requirements#hardware-sizing)

One of the following desktop browsers is required to use the web management console:

- Latest two Chrome versions
- Latest two Firefox versions
- Latest two Microsoft Edge versions

Mobile layouts are not supported yet.

## [MetaDefender OT Access Gateway](/docs/metadefender-ot-access/2.3.2/system-requirements/system-requirements#minimum-hardware-requirement)

Windows system-level service that can be used as an alternative to the Windows Client. The service launches automatically when the system boots. OT Access Service also work as the Endpoint Gateway.

### [Hardware sizing](/docs/metadefender-ot-access/2.3.2/system-requirements/system-requirements#metadefender-ot-access-client)

| Concurrent Sessions per Gateway | CPU | RAM | Hard Disk |
| --- | --- | --- | --- |
| Up to 25 | 1 CPU ( 2 cores) | 4 GB | 64 GB |
| Up to 100 | 1 CPU ( 4 cores) | 8 GB | 128 GB |
| Up to 500 | 1 CPU ( 8 cores) | 16 GB | 128 GB |

## [MetaDefender OT Access Client](/docs/metadefender-ot-access/2.3.2/system-requirements/system-requirements#software-requirement)

Connect the Remote User's computer to the Cloud or the Management Console and ultimately to their OT Endpoint Devices. OT Access Console also work as the Endpoint Gateway.

### [Minimum Hardware Requirement](/docs/metadefender-ot-access/2.3.2/system-requirements/system-requirements#minimum-hardware-requirement)

| RAM | 4 GB |
| --- | --- |
| CPU | 1 CPU (2 cores) |
| Hard disk | 64 GB |

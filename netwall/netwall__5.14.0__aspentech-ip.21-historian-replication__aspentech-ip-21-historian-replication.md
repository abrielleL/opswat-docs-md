<!-- source: https://www.opswat.com/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication -->

# Aspentech IP.21 Historian Replication with MSMQ.

You need MetaDefender Bilateral Security Gateway to perform Aspentech IP.21 Historian replication

**Introduction**

This document describes how to configure MetaDefender Security Gateway and an Aspentech IP.21 database, Version 8 and above, to enable database replication from a Publisher database to a Subscriber database.

This document is intended as a companion to the following:

- *MetaDefender Security Gateway User Guide*: Refer to this User Guide for information on installing the MetaDefender Security Gateway hardware and software and initial configuration of the MetaDefender Security Gateway nodes.
- A [Aspentech esupport](https://esupport.aspentech.com/S_Login?startURL=%2FS_Article%3Fid%3D000077421): Refer to this site in general for information on configuring data and tag replication. Specifically, refer to the article “How do I configure Aspen InforPlus.21 V8.0 (and above) Data and Tag Replication?”

The configuration will create a bilateral TCP connection between the databases and MetaDefender Security Gateway.

## <**Configuration**>

### <**Prerequisites**>

We need to comply with the following requirements:

- Install and configure MetaDefender Security Gateway: Follow the instructions in the *MetaDefender Security Gateway User Guide* to install MetaDefender Security Gateway and configure the MetaDefender Security Gateway RED and BLUE nodes.
- Ensure Microsoft Message Queue (MSMQ) Server is installed on both Provider and the Subscriber systems.

### [**Configure streaming point parameters**](/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication#configure-streaming-point-parameters)

Follow the instructions in the MetaDefender Security Gateway *User Guide* to configure the streaming point parameters. These parameters connect the MetaDefender Security Gatewayl BLUE and RED nodes to the Aspentech databases and determine replication.

After you complete your configuration, the connections should appear as shown in the following image. The IP. 21 PCs are Aspentech databases. The Publisher database connects to MetaDefender Security Gateway BLUE and the Subscriber database connects to MetaDefender Security Gateway RED.

Note

Port number must be 1801, which is the port used by MSMQ

### [MetaDefender Security Gateway Blue Configuration](/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication#metadefender-security-gateway-blue-configuration)

Please, check the screenshots for MetaDefender Security Gateway BLUE configuration:

### [MetaDefender Security Gateway Red Configuration](/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication#metadefender-security-gateway-red-configuration)

Please, check the screenshots for MetaDefender Security Gateway RED configuration:

### [**Configure Publisher database**](/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication#configure-publisher-database)

This section describes how to configure the Publisher database to transfer data to the Subscriber database for replication. Refer to the Aspentech support site for assistance.

Configuration steps:

- Add task(s) to replicate.
- Enable global replication.
- Add subscriber record.

Notes

All configuration steps are performed on the Publisher database system (NOT MetaDefender Security Gateway).The IP addresses shown in the images below are representative only.

#### [**Add task**](/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication#add-task)

Select the task(s) on the Publisher database that you want to replicate.

#### [**Enable global replication**](/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication#enable-global-replication)

In the Administrator, right-click the IP of the Publisher database and select **Properties**. Click to select *Enable global replication for this IP21 database.*

#### [**Add Subscriber record**](/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication#add-subscriber-record)

The Subscriber record on the Publisher database links to the data and tags on the Subscriber database. Click to select the record in the **RepSubscriberdef** folder.

Info

The record name is an example. **RepSubscriberDef** is the correct name of the folder.

### [**Configure Subscriber database**](/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication#configure-subscriber-database)

This section describes how to configure the Subscriber database to replicate data received from the Publisher database. Refer to the Aspentech support site for assistance.

Configuration steps:

- Add task(s) that will be replicated
- Ensure global replication is NOT enabled
- Add subscriber record

Note

All configuration steps are performed on the Subscriber database system (NOT MetaDefender Security Gateway).

The IP addresses shown in the images below are representative only.

#### [**Add task**](/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication#add-task)

Select the task(s) you want to replicate.

#### [**Ensure global replication is NOT enabled**](/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication#ensure-global-replication-is-not-enabled)

Global replication must be enabled on the Publisher database system, but must **NOT** be enabled on the Subscriber database system.

In the Administrator, right-click the IP of the Subscriber database and select **Properties**. Ensure ‘Enable global replication for this IP21 database’ is NOT selected.

#### [**Add Subscriber record**](/docs/netwall/5.14.0/aspentech-ip.21-historian-replication/aspentech-ip-21-historian-replication#add-subscriber-record)

The Subscriber record on the Subscriber database links to the data and tags on the Pubisher database. Click to select the record in the **RepPublisherdef** folder.

Note

The record name is an example. **RepPublisherDef** is the correct name of the folder.

<!-- source: https://www.opswat.com/docs/netwalldiode/oracle-goldengate-database-replication/oracle-goldengate-database-replication -->

# Oracle GoldenGate Database Replication

This document is a guide for implementation of configuration steps needed to perform Oracle GoldenGate Database replication from OT (BLUE zone) to IT (RED zone) using MetaDefender Optical Diode.

The document assumes the reader is familiar with Oracle Database and Oracle GoldenGate products. The document assumes the reader is familiar with the tasks associated with creating Oracle GoldenGate EXTRACT and Oracle GoldenGate REPLICAT as well as configuring the Oracle Databases for successful replication via Oracle GoldenGate. It provides guideline on the extra tasks needed to configure NetWall product family to provide transport services for Oracle GoldenGate.

You will need to know the IP address/port of the Oracle GoldenGate Server(s). You will need to know the IP addresses of the MetaDefender Optical Diode BLUE and MetaDefender Optical Diode RED. You will also need to be able to make changes to both MetaDefender Optical Diode appliances’ configuration. In addition, you will need to know the folder locations of the pre-configured EXTRACT (BLUE zone) and REPLICAT (RED zone) Oracle GoldenGate elements and credentials for accessing these locations on each zone.

The locations of the trail files are defined when creating EXTRACT / REPLICAT services during Oracle GoldenGate configuration. Record these locations so these can be used later by MetaDefender Optical Diode.

Example of the environment

## [Tasks associated with Source/Destination preparation](/docs/netwalldiode/oracle-goldengate-database-replication/oracle-goldengate-database-replication#tasks-associated-with-sourcedestination-preparation)

When performing Oracle GoldenGate replication MetaDefender Optical Diode is simply transport mechanism. In a sense, a replacement for the Oracle GoldenGate MGR service. Thus, there are various ways to transfer the files across the domain. The choices are: FTP/FTPS, SFTP or Windows File Share. For each of these methods, credentials will be needed as well as preparing the source/destination (e.g. Share Path). The steps to make these accessible are responsibility of the corresponding system administrators.

In addition, if you choose FTP/FTPS as a transport protocol, the FTP service on the corresponding servers needs to be tuned up in order to accommodate the NetWall product family requirements.

## [Configuring your OT Oracle Database/Oracle GoldenGate (BLUE)](/docs/netwalldiode/oracle-goldengate-database-replication/oracle-goldengate-database-replication#configuring-your-ot-oracle-databaseoracle-goldengate-blue)

Follow the steps defined by Oracle to configure the replication of the database of your choice. Follow the steps defined by Oracle GoldenGate to configure EXTRACT of your choice. Note the location to which your EXTRACT will dump the files. In this example, these are the parameters:

- IP address of the Oracle Database/Oracle GoldenGate server: 192.168.101.252
- EXTRACT extopsw: /u01/app/goldengate/21.3.0.0/dirdat
- User: oracle
- Password: <your chosen password>

## [Configuring your MetaDefender Optical Diode BLUE for FTPS transfers](/docs/netwalldiode/oracle-goldengate-database-replication/oracle-goldengate-database-replication#configuring-your-metadefender-optical-diode-blue-for-ftps-transfers)

- Connect to MetaDefender Optical Diode (BLUE) and login.
- Select File Transfers -> FTP -> Add FTP Share - for example:
- Fill-in the required fields
- Ensure “Delete Files on Share after transfer” is unchecked
- Ensure “Preserve file timestamp” is checked
- Save the configuration and proceed to RED

This concludes MetaDefender Optical Diode BLUE configuration.

## [Configuring your IT Oracle Database/Oracle GoldenGate (RED)](/docs/netwalldiode/oracle-goldengate-database-replication/oracle-goldengate-database-replication#configuring-your-it-oracle-databaseoracle-goldengate-red)

Follow the steps defined by Oracle to configure the replication of the database of your choice. Follow the steps defined by Oracle GoldenGate to configure REPLICAT of your choice. Note the location to which your REPLICAT will dump the files. In this example, these are the parameters:

- IP address of the Oracle Database/Oracle GoldenGate server: 192.168.222.252
- REPLICAT repopsw: /u01/app/goldengate/21.3.0.0/dirdat
- User: oracle
- Password: <your chosen password>

## [Configuring your MetaDefender Optical Diode (RED)](/docs/netwalldiode/oracle-goldengate-database-replication/oracle-goldengate-database-replication#configuring-your-metadefender-optical-diode-red)

- Connect to MetaDefender Optical Diode (RED) and login.
- Select File Transfers -> FTP -> Add FTP Share - for example:
- Fill-in the required fields
- Ensure “Preserver file timestamp” checkbox is checked.
- Save the configuration.

This concludes MetaDefender Optical Diode RED configuration.

MetaDefender

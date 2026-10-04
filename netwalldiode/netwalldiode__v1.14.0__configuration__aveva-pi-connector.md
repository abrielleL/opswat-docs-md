<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector -->

# AVEVA PI Connector

The NetWall AVEVA Pi Connector extracts values, PI point schema and pertinent Digital State Tables from one or more PI systems in the source (BLUE) domain and stores those values on a designated PI system in the destination (RED) domain.

The Pi Connector also performs historical backfill. Historical backfill alleviates any gaps in archive data on the destination PI system.

### [Installation Prerequisites](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#installation-prerequisites)

It is recommended to install the NetWall AVEVA-PI Service software either on the PI server itself or on an API node that is on a network local to the PI server. This will eliminate any delays that could be caused by increased latency if the NetWall AVEVA PI Service were to be located on a remote network with limited bandwidth.

The NetWall AVEVA PI Service software has been tested on Windows 10, Windows 11, Windows Server 2012 R2, Windows Server 2019 and Windows Server 2022.

Important

NetWall AVEVA PI Service is a 64 bits application and can't be installed in 32 bits machines.

Please, check the system requirements for an independent node depending on the number of Pi points you need to manage in the table below. Additional resources are required if the AVEVA PI client is installed on the same machine as the PI server:

| Database Points | CPU | RAM |
| --- | --- | --- |
| 10000 | 2 | 8G |
| 50000 | 2 | 8G |
| 100000 | 4 | 12G |
| 250000 | 4+ | 16G |

The NetWall AVEVA PI Service uses the PI Asset Framework SDK. The PI AF Client must be installed on the machine where the NetWall AVEVA PI Service is to be installed. The following versions of the AF SDK have been tested:

- PI-AF-Cient_2023_.exe
- PI-AF-Client_2018-SP3-Patch-5_.exe
- PI-AF-Client_2018-SP3-Patch-3_.exe

Note that older versions of PI (3.4.390) can be read by the NetWall AVEVA PI Software but cannot be written to. If an older version of PI is to be used as the source (BLUE) database, you must create a separate API node and install the AF SDK and the NetWall AVEVA PI Service. You can then either create a PI trust or create a PI mapping to access the data in the PI database from the API node.

### [Pi Collectives](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#pi-collectives)

The NetWall AVEVA Pi Connector supports Pi Collectives. Two or more PI databases can be configured as a redundant set. This redundant set is called a Collective. The Collective is normally created in a specified domain, and each PI database is operating on a computer that is a member of that domain. Every collective has a Primary PI Database member, and one or more secondary PI Database members.

## [PI2PI](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#pi2pi)

### [PI2PI-Blue Service](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#pi2pi-blue-service)

*NetWall AVEVA PI Service (BLUE)* needs to be installed on each PI server of interest on the BLUE network. It operates as a Windows Service, configuration for the PI2PI system is done using the Optical Diode Web UI on Blue and the Web Ui on Red. There is no user interface on the Windows machines. *NetWall AVEVA PI Service (BLUE)* service can be loaded either on the PI server itself or on another Windows machine that has the PI SDK installed and has a trusted relationship with the PI Server. To correctly install it, follow the instructions:

1. Double click on the msi file that OPSWAT will provide *NetWall AVEVA PI Service (BLUE)* and click Next.
2. Fill in the IP address and port for listening for the configuration and click Next. Typically, this IP will be the IP of Optical Diode BLUE.
3. Click finish button to exit the Setup.

### [Optical Diode BLUE](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#optical-diode-blue)

Important

A security dongle must be inserted in the BLUE side to change configuration.

1. Login into MetaDefender Optical Diode BLUE.
2. Go to AVEVA PI menu, select Pi to PI label, deploy Action button and select Add Client.
3. Type values in the following boxes:

   1. **Flanker IP:** IP address of the Blue Windows Machine.
   2. **Flanker Port Config:** Port number the Blue Windows Machine is listening on for Config.
   3. **Flanker Name:** In case of redundancy, name for the first flanker.
   4. **Second Flanker IP:** In case of redundancy, IP address of the second flanker.
   5. **Second Flanker Port Config:** In case of redundancy, port number where the second flanker defined will listen on for configuration.
   6. **Flanker Name:** In case of redundancy, name for the second flanker.
   7. **Pi Tag Preferred Flanker:** You can choose which Flanker is preferred (active). Create a PI Tag(string) and update the value with one of the names chosen in **Flanker Name**. Fill in the PI Tag name in this field.
   8. **Instance**: The Interface Instance number to be used at red. Must be a positive integer.
   9. **Backfill Max Records/sec:** Max values per second to extract during backfill (range: 1000-20000).
   10. **Backfill Slice (m):** The number of minutes to read for each History Backfill retrieval (range: 1-60).
   11. **Point Prepend:** Prepend the string indicated here to each Pi point. The maximum length for the string is 20 chars (lowercase, uppercase, numbers, dash and undescore are allowed characters).
   12. **Stats Prepend:** If this field is not empty, then the structure of the PI tags used to publish the statistics will be: opswat_blue_{stats prepend value}_{PI tag name}. If this field is empty, then the interface instance is used instead of stats prepend value.
   13. **Source Tag Select:** Dropdown list where the user can select between Exact Tag Name, Instrument Tag, ExDesc and UserInt1.
   14. **Backfill Time (HH):** How far back in time to go for historical backfill (range: 0.5-168, values with more than two decimals will be rounded).
   15. **Database Name :** Windows Network Name of the PI server.
   16. **User:** PI Username (blank: use trusted connection).
   17. **Password:** PI Password (blank: use trusted connection).
   18. **Debug Points:** Points for debugging, separated by semicolon ';'. Maximum 10 points.
   19. **Debug Mode:** User can select the debug mode using this dropdown list. User can select between Disabled, All, Snapshot only and History only.
   20. **Debug Detail:** User can select the debug detail using this dropdown list. User can select between Count only and List History values.
   21. **Point Sources:** One or more PI point sources, separated with semicolon ';'.
   22. **Point Filter Name:** User can assign a Pi field to use for additional point filtering in BLUE. "None" means no filter.
   23. **Point Table Refresh Rate:** Rate in hours for transmitting the PI Point Table. Range is from 0.2 to 2.
   24. **Schema Records per Second:** Maximun number of Schema records to transmit per second (default value is 2000, range is from 1000 to 5000).
   25. **Statistics Seconds:** Statistics frequency in seconds. If the value is 0, no statistics are printed (range: 5-3600).
   26. **Use Location1:** If 'Yes' is selected, Location1 on Red must match Instance.
   27. **Description:** user-friendly description for the defined Client.
4. Click on Submit button to save the changes.

### [PI2PI-Red Service](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#pi2pi-red-service)

*NetWall AVEVA PI service (RED)* needs to be installed on the PI server on the RED network. It operates as a Windows Service, configuration for the Pi2PI system is done using the OPSWAT Web interface on Blue and the Web UI on Red. There is no user interface on the Windows machines. *NetWall AVEVA PI service (RED)* can be loaded either on the PI server itself or on another Windows machine that has the PI SDK installed and has a trusted relationship with the PI Server. To correctly install it, follow the instructions:

1. Double click on the msi file that OPSWAT will provide *OPSWAT NetWall AVEVA PI Service (RED)* and click Next.
2. Fill in the IP address and port for listening for the configuration and click Next. Typically, this IP will be the IP of Optical Diode RED.
3. Click finish button to exit the Setup.

### [Optical Diode RED](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#optical-diode-red)

Important

A security dongle must be inserted in the RED side to change configuration.

1. Login into Optical Diode RED.
2. Go to AVEVA PI menu and click on Edit button. Notice that only one AVEVA PI Client can be configured in Optical Diode RED.
3. **Type values in the following boxes:**

   1. **Flanker IP:** IP address of the Windows Machine in the RED network acting as flanker.
   2. **Flanker Port Config:** Port number where the flanker defined will listen on for configuration.
   3. **Flanker Port Data:** Port number where the defined flanker will listen on for data transmission.
   4. **Second Flanker IP:** In case of redundancy, IP address of the second flanker.
   5. **Flanker Port Config:** In case of redundancy, port number where the second flanker defined will listen on for configuration.
   6. **Flanker Name:** In case of redundancy, name for the second Flanker
   7. **Pi Tag Preferred Flanker:** You can choose which Flanker is preferred (active). Create a PI Tag(string) and update the value with one of the names chosen in **Flanker Name**. Fill in the PI Tag name in this field.
   8. **Stats Prepend:** If this field is not empty, then the structure of the PI tags used to publish the statistics will be: opswat_blue_{stats prepend value}_{PI tag name}. If this field is empty, then the interface instance is used instead of stats prepend value.
   9. **Database Name:** PI Server name within the Windows Network.
   10. **User:** PI username (leave it blank for using a trusted connection).
   11. **Password:** PI password (leave it blank for using a trusted connection).
   12. **Point Sources:** User can include here one or more Pi point souces seperated with semicolon.
   13. **Debug Points:** A maximum number of 10 debugging points can be configured including them in this field separated by semicolon ';'.
   14. **Debug Mode:** User can select the debug mode using this dropdown list. User can select between Disabled, All, Snapshot only and History only.
   15. **Debug details:** User can select the debug detail using this dropdown list. User can select between Count only and List History values.
   16. **Statistics Seconds:** Statistics frequency in seconds. If the value is 0, no statistics are displayed.
   17. **Description:** User-friendly description field for the created client.
4. Click on Submit button to save the changes.

## [PI Database Replication](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#pi-database-replication)

### [AVEVA PI DB replication Service (BLUE)](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#aveva-pi-db-replication-service-blue)

NetWall AVEVA PI DB replication service (BLUE) needs to be installed on each PI server of interest on the BLUE network. It operates as a Windows Service, configuration for the DB Replication system is done using the OPSWAT Web interface on Blue and the OPSWAT Web interface on Red. There is no user interface on the Windows machines. NetWall AVEVA PI DB replication service (BLUE) service can be loaded either on the PI server itself or on another Windows machine that has the PI SDK installed and has a trusted relationship with the PI Server. To correctly install it, follow the instructions:

1. Double click on the msi file that OPSWAT will provide *OPSWAT NetWall AVEVA PI replication Service (BLUE)* and click Next.
2. Fill in the IP address and port for listening for the configuration and click Next. Typically, this IP will be the IP of Optical Diode BLUE.

3. Click finish button to exit the Setup.

### [Optical Diode BLUE](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#optical-diode-blue)

Important

To configure AVEVA PI Connector, a security dongle must be inserted in the BLUE server.

1. Login into Optical Diode BLUE.
2. Go to AVEVA PI menu deploy Action button and select Add Client.
3. Type values in the following boxes:

   1. **Flanker IP:** IP address of the Blue Windows Machine.
   2. **Flanker Port Config:** Port number the Blue Windows Machine is listening on for Config.
   3. **Flanker Name:** Name of the flanker.
   4. **Second Flanker IP:** In case of redundancy, IP address of the second flanker.
   5. **Flanker Port Config:** In case of redundancy, port number where the second flanker defined will listen on for configuration.
   6. **Flanker Name:** In case of redundancy, name of the second flanker.
   7. **Pi Tag Preferred Flanker:** You can choose which Flanker is preferred (active). Create a PI Tag(string) and update the value with one of the names chosen in **Flanker Name**. Fill in the PI Tag name in this field.
   8. **Instance**: The Interface Instance number to be used at red. Must be a positive integer.
   9. **Backfill Max Records/sec:** Max values per second to extract during backfill (range: 1000-20000).
   10. **Backfill Slice (m):** The number of minutes to read for each History Backfill retrieval (range: 1-60).
   11. **Point Prepend:** Prepend the string indicated here to each Pi point. The maximum length for the string is 20 chars (lowercase, uppercase, numbers, dash and undescore are allowed characters).
   12. **Point Append:** Append the string indicated here to each PI point. Maximum lenght is 20 characters. (lowercase, uppercase, numbers, dash and undescore are allowed characters).
   13. **Stats Prepend:** If this field is not empty, then the structure of the PI tags used to publish the statistics will be: opswat_blue_{stats prepend value}_{PI tag name}. If this field is empty, then the interface instance is used instead of stats prepend value.
   14. **Backfill Time (HH):** How far back in time to go for historical backfill (range: 0.5-168, values with more than two decimals will be rounded).
   15. **Database Name :** Windows Network Name of the PI server.
   16. **User:** PI Username (blank: use trusted connection).
   17. **Password:** PI Password (blank: use trusted connection).
   18. **Debug Points:** Points for debugging, separated by semicolon ';'. Maximum 10 points.
   19. **Debug Mode:** User can select the debug mode using this dropdown list. User can select between Disabled, All, Snapshot only and History only.
   20. **Debug Detail:** User can select the debug detail using this dropdown list. User can select between Count only and List History values.
   21. **Point Sources:** One or more PI point sources, separated with semicolon ';'.
   22. **Point Filter Name:** Allows filtering on attributes in addition to Point Sources.
   23. **Point Table Refresh Rate:** Rate in hours for transmitting the PI Point Table. Valid values are 0.2-2.
   24. **Schema Records per Second:** Maximum number of Schema records to transmitper second. Valid values are 1000-5000.
   25. **Statistics Seconds:** Statistics frequency in seconds. If the value is 0 no statistics are printed. Valid values are 5-3600, default value is 60 seconds.
   26. **Enabled:** This checkbox should be marked to enable AVEVA PI connector.
4. Click on Submit button to save the changes.

### [AVEVA PI DB Replication Service (RED)](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#aveva-pi-db-replication-service-red)

NetWall AVEVA PI DB replication service (RED) needs to be installed on the PI server on the RED network. It operates as a Windows Service, configuration for the DB Replication system is done using the Optical Diode Web UI on Blue and ton Red. There is no user interface on the Windows machines. NetWall AVEVA PI DB replication service (RED) service can be loaded either on the PI server itself or on another Windows machine that has the PI SDK installed and has a trusted relationship with the PI Server. To correctly install it, follow the instructions:

1. double click on the msi file that OPSWAT will provide *NetWall AVEVA PI replication Service (RED)* and click Next.
2. Fill in the IP address and port for listening for the configuration and click Next. Typically, this IP will be the IP of Optical Diode RED.
3. Click finish button to exit the Setup.

### [Optical Diode RED](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#optical-diode-red)

Important

To configure AVEVA PI Connector, a security dongle must be inserted in the RED server

1. Login into NetWall RED.
2. Go to AVEVA PI menu and click on **Edit** button. Notice that only one AVEVA PI Client can be configured in Optical Diode RED.
3. **Type values in the following boxes:**

   1. **Flanker IP:** IP address of the Windows Machine in the RED network acting as flanker.
   2. **Flanker Config Port:** Port number where the flanker defined will listen on for configuration.
   3. **Flanker Data Port:** Port number where the defined flanker will listen on for data transmission.
   4. **Name:** Name of the flanker.
   5. **Second Flanker IP:** In case of redundancy, IP address of the second flanker.
   6. **Config Port:** In case of redundancy, port number where the second flanker defined will listen on for configuration.
   7. **Data Port:** In case of redundancy, port number where the second flanker will listen on for data transmission.
   8. **Name:** In case of redundancy, name of the second flanker.
   9. **Pi Tag Preferred Flanker:** You can choose which Flanker is preferred (active). Create a PI Tag(string) and update the value with one of the names chosen in **Flanker Name**. Fill in the PI Tag name in this field.
   10. **Stats Prepend:** If this field is not empty, then the structure of the PI tags used to publish the statistics will be: opswat_blue_{stats prepend value}_{PI tag name}. If this field is empty, then the interface instance is used instead of stats prepend value.
   11. **Database Name:** PI Server name within the Windows Network.
   12. **User:** PI username (leave it blank for using a trusted connection).
   13. **Password:** PI password (leave it blank for using a trusted connection).
   14. **Point Sources:** User can include here one or more Pi point souces seperated with semicolon.
   15. **Debug Points:** A maximum number of 10 debugging points can be configured including them in this field separated by semicolon ';'.
   16. **Debug Mode:** User can select the debug mode using this dropdown list. User can select between Disabled, All, Snapshot only and History only.
   17. **Debug details:** User can select the debug detail using this dropdown list. User can select between Count only and List History values.
   18. **Statistics Seconds:** Statistics frequency in seconds. If the value is 0, no statistics are displayed.
   19. **Description:** User-friendly description field for the created client.
   20. **Attribute Blocking:** Identify one or more attributes that are not to be replicated on Red. This applies to all points.
4. Click on Submit button to save the changes.

## [Optimizing AVEVA Pi Connector Historical Backfill](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#optimizing-aveva-pi-connector-historical-backfill)

The AVEVA Pi Connector-Blue collects historical data and sends it to Red. AVEVA Pi-Blue is constrained by the maximum number of values per second that it is allowed to send to Red. If AVEVA Pi-Blue is unable to complete an entire history cycle in less time than the specified History Time Span, then a *History Overrun* condition exists. Click on this link for tips on [Optimizing AVEVA Pi Historical Backfill](/docs/netwalldiode/v1.14.0/optimizing-aveva-pi-historical-backl/optimizing-aveva-pi-historical-backl).

## [Partial Historical Backfill by Date/Time Range](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#partial-historical-backfill-by-datetime-range)

Users can do a partial historical backfill for a specified time and for a selected number of Pi points. That can be done for both, Pi2Pi and Pi Database Replication.

To perform a partial historical backfill go to **Connector -> AVEVA Pi** and select a **Pi Replication or Pi2Pi**. Then select one entry on the table and the Edit view will be displayed. Click on Update Partial History button.

A pop up will appear to indicate the date and the Pi points to perform the backfill.

Info

Updating the Partial History Backfill for a flanker will restart any Partial Backfill already in progress for that flanker.

Once the user have selected **Start time, End Time and Points**, Click on the **Submit** button to start Backfill.

## [AVEVA PI Multi-Site High Availability Configuration](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#aveva-pi-multi-site-high-availability-configuration)

Info

If an AVEVA Pi multi-site high availability system required, additional configuration is needed. Please, follow the instructions bellow.

Go to the High Availability tab and fill in the following fields:

1. **Site A Name:** Name of geographic Site A.
2. **Site A Heartbeat Pi Tag:** Define an existing Pi Tag in the Site A as Heartbeat.
3. **Site B Name:** Name of geographic Site B.
4. **Site B Heartbeat Pi Tag:** Define an existing Pi Tag in the Site B as Heartbeat.
5. **My Site:** Select the Site (A or B) this NetWall is connected to.
6. **Preferred Pi Tag:** Pi Tag used in the system's preferred site
7. **Enable:** Tick the checkbox to enable High Availability configuration for redundant systems.

Click on Submit button to save the changes.

## [Statistics](/docs/netwalldiode/v1.14.0/configuration/aveva-pi-connector#statistics)

Users can check AVEVA PI Statistics by clicking on the Statistics tab in AVEVA PI Connector section of the menu.

MetaDefender

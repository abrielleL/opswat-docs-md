<!-- source: https://www.opswat.com/docs/netwall/5.14.0/configuration/a-iec0194-connector -->

# IEC-104 Connector

View as Markdown Ask ChatGPT about this page Ask Claude about this page

IEC 104 Connector allows you to transfer IEC-104 data unidirectionally across the MetaDefender Optical Diode. The IEC-104 Connector is configured on the Optical Diode BLUE and RED side.

The IEC-104 Connector on the Optical Diode BLUE collects data from customer-owned IEC-104 controlled stations in the BLUE zone and transfers that data to the IEC-104 Connector configured on the Optical Diode RED. Customer-owned IEC-104 controlling stations in the RED zone connect to the IEC-104 Connector to monitor the transferred data.

Info

Please, take into consideration that APDUs with time tag will only be received on the RED side with Cause of Transmission set to Spontaneous.> > APDUs that could be affected by this are:> > MSPNA1=1, MSPTA1=2, MDPNA1=3, MDPTA1=4, MSTNA1=5, MSTTA1=6, MBONA1=7, MBOTA1=8, MMENA1=9, MMETA1=10, MMENB1=11, MMETB1=12, MMENC1=13, MMETC1=14, MITNA1=15, MITTA1=16, MEPTA1=17, MEPTB1=18, MEPTC1=19, MPSNA1=20, MMEND1=21, MSPTB1=30, MDPTB1=31, MSTTB1=32, MBOTB1=33,MMETD1=34, MMETE1=35, MMETF1=36, MITTB1=37, MEPTD1=38, MEPTE1=39, MEPTF1=40, PMENA1=110, PMENB1=111, PMENC_1=112.

### [Optical Diode BLUE](/docs/netwall/5.14.0/configuration/a-iec0194-connector#optical-diode-blue)

Info

A security dongle must be inserted in the BLUE and RED servers to change configuration.

Navigate to the **IEC104 menu item** under the **Connectors** menu, In the **Action** menu, select **Add Controlling Station**.

1. Type values in the following boxes:
2. 1. **Station # (Channel):** Channel of the IEC-104 stream, this should be the same channel in both BLUE and RED sides.
   2. **Controlled Station IP:** IP address of the customer-owned IEC 104 Controlled station that the IEC-104 Connector will collect data from.
   3. **Controlled Station Port**: IEC-104 port of the controlled station on the IEC-104 Connector. Default: 2404.
   4. **Originator address:** IEC-104 address to identify the originator. Valid values are from 1 to 255.
   5. **Common Address:** Is the application address of the client (logical station) that must match the address defined in the client configuration. This is defined as the address of the controlling station in the control direction. Valid values are from 1 to 65536.
   6. **Connection Timeout (t0):** Default value for connection establishment timeout is 30 secs. Valid values are from 1 to 255 secs.
   7. **Send/Request Timeout (t1):** Default value for sending or testing APDUs is 15 secs. Valid values are from 1 to 255 secs.
   8. **Acknowledge Timeout (t2):** This is a timeout for acknowledges in case of no data messages and the default value is 10 secs. Valid values are from 1 to 255 secs.
   9. **Test Frame Timeout (t3):** Timeout for sending test frames in case of a long idle state. Default value is 20 secs and valid values are from 1 to 172801 secs.
   10. **Max Outstanding APDUs (k):** The IEC-104 client does not send more APDUs if the maximum number of ADPUs have been transmitted and have not been acknowledged. The default value is 12 APDUs.
   11. **Max Latest Acknowledge APDUs (w):** This setting works in conjunction with t2 to limit how often the IEC-104 client acknowledges APDUs. Increasing this setting can reduce bandwidth required for acknowledging. Default value is 8 APDUs.
3. Click the **Submit** button to save the changes.

### [Optical Diode RED](/docs/netwall/5.14.0/configuration/a-iec0194-connector#optical-diode-red)

Info

A security dongle must be inserted in the BLUE and RED servers to change configuration.

Navigate to the **IEC104 menu item** under the **Connectors** menu, In the **Action** menu, select **Add Controlled Station**.

1. **Type values in the following boxes:**
2. 1. **Station # (Channel):** Channel of the IEC-04 stream, this should be the same channel in both sides, RED and BLUE.
   2. **Allowed Controlling Station IP:** IP address of the customer-owned IEC-104 Controlling station OPSWAT IEC-104 connector will collect data from. Several controlling stations can be configured.
   3. **Controlled Station Port**: IEC-104 port on the OPSWAT IEC-104 connector.
   4. **Common address:** In the RED side originator and common addresses have to share the same value. Valid values are from 1 to 65334.
   5. **Max Open Connection:** Max. number of controlling stations that can be connected simultaneously.
   6. **Connection Timeout (t0):** Default value for connection establishment timeout is 30 secs. Valid values are from 1 to 255 secs.
   7. **Send/Request Timeout (t1):** Default value for sending or testing APDUs is 15 secs. Valid values are from 1 to 255 secs.
   8. **Acknowledge Timeout (t2):** This is a timeout for acknowledges in case of no data messages and the default value is 10 secs. Valid values are from 1 to 255 secs.
   9. **Test Frame Timeout (t3):** Timeout for sending test frames in case of a long idle state. Default value is 20 secs and valid values are from 1 to 172801 secs.
   10. **Max Outstanding APDUs (k):** The IEC 104 client does not send more APDUs if the maximum number of ADPUs have been transmitted and have not been acknowledged. The default value is 12 APDUs.
   11. **Max Latest Acknowledge APDUs (w):** This setting works in conjunction with t2 to limit how often the IEC 104 client acknowledges APDUs. Increasing this setting can reduce bandwidth required for acknowledging. Default value is 8 APDUs.
   12. **Enabled: IEC 104** Connector can be enabled/disabled using this checkbox
3. Click the **Submit** button to save the changes.

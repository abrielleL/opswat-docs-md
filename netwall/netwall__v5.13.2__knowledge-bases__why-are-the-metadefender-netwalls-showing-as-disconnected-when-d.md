<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/knowledge-bases/why-are-the-metadefender-netwalls-showing-as-disconnected-when-d -->

# Why are the Metadefender Netwalls showing as disconnected when data cable is in use.

This article applies to BSG USG Netwall devices.

When the Metadefender Netwalls are in use, and the Management Consoles on both the Blue and Red units report that Link 0 is in a DISABLED state, showing the following:

Blue Netwall Management console:

Red Netwall Management Console:

And from the exported logs of the units, the following entries appear inside the dolphin_dis_diag.txt file for both devices:

**Blue Netwall – MXH ADAPTER 0 LINK 0 STATE**

************************* MXH ADAPTER 0 LINK 0 STATE *************************
Link 0 downtime : 42 seconds
Link 0 state : DISABLED
Link 0 required : x4, Gen4 (16 GT/s)
Link 0 capabilities : x4, Gen4 (16 GT/s)
Link 0 hwport : P32
Link 0 cable inserted : 0
Link 0 configuration : NTB

**Red Netwall – MXH ADAPTER 0 LINK 0 STATE**

************************* MXH ADAPTER 0 LINK 0 STATE *************************
Link 0 downtime : 164 seconds
Link 0 state : DISABLED
Link 0 required : x4, Gen4 (16 GT/s)
Link 0 capabilities : x4, Gen4 (16 GT/s)
Link 0 hwport : P32
Link 0 cable inserted : 0
Link 0 configuration : NTB

Please confirm that the cable is seated correctly and tightly in both units. In case the cable is not correctly connected all the way into the units without any kind of movement or looseness.

Please proceed to contact Opswat support for further troubleshooting.

Support

If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support-services).

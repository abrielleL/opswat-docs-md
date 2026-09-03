<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/how-do-i-send-radius-accounting-to-nac-for-ruckus-wir -->

# How do I send RADIUS Accounting to NAC for Ruckus Wireless?

This article applies to the current NAC Enforcer.

1. **Add NAC Authentication and a NAC Accounting Server as follows.**

   - For the **RADIUS Accounting Server**, set the **IP Address** field to the IP address of your **NAC Enforcer** or, in a cluster, enter the **Manager’s** IP address.
   - Enter a **Name** for the **RADIUS Server**.
   - Set the **Type** to **RADIUS Accounting**.
   - Set the **Port** to **1813**.
   - Enter the desired value for the **Secret**.
   - Click **OK**

2. **Edit your existing WLANs/ESSIDs as follows.**

   - Edit your **WPA2-Enterprise WLAN**.
   - Expand the **Advanced Actions** section.
   - From the drop-down menu, set the **Accounting Server** to the **NAC** **Accounting Server** that you created earlier.

Support:

If you have followed the instructions above but have been unable to **Send RADIUS Accounting To NAC For Ruckus Wireless**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

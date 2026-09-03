<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/how-do-i-send-radius-accounting-to-nac-for-cisco-meraki -->

# How do I send RADIUS Accounting to NAC for Cisco Meraki?

This article applies to the current NAC Enforcer, the Web UI and the current NAC Policy Key deployed on Windows and Linux systems.

**Edit your existing WPA2I SSID as follows.**

- Enable **RADIUS** **Accounting**.
- Set the RADIUS accounting server **Host** field to the IP address of your NAC appliance.
- Set the **Port** to **1813**.
- Enter the desired value in the **Secret** field.
- Click **Save** to enable your **WPA2E SSID**.

Support:

If you have followed the instructions above but have been unable to **Send RADIUS Accounting To NAC For Cisco Meraki**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

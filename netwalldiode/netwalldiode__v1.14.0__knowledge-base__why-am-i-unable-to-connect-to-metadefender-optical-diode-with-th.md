<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/knowledge-base/why-am-i-unable-to-connect-to-metadefender-optical-diode-with-th -->

# Why am I unable to connect to MetaDefender Optical Diode with the Default IP Address?

Users may encounter issues connecting to the MetaDefender Optical Diode when the client device is not configured with compatible network settings.

The issue is typically due to incorrect manual IP configuration on the user's machine, such as mismatched IP address range or incorrect subnet mask.

### [Prerequisites:](/docs/netwalldiode/v1.14.0/knowledge-base/why-am-i-unable-to-connect-to-metadefender-optical-diode-with-th#prerequisites)

- A Windows laptop or PC
- Administrative access to modify network settings
- A straight-through Ethernet cable (crossover cable is not required)

### [Symptoms:](/docs/netwalldiode/v1.14.0/knowledge-base/why-am-i-unable-to-connect-to-metadefender-optical-diode-with-th#symptoms)

- Inability to access the Netwall web interface via browser
- MetaDefender Netwall unreachable at default IP `https://10.10.10.10`
- "Unable to connect" browser errors despite correct cabling
- No response from Netwall when pinged

### [Resolution Steps:](/docs/netwalldiode/v1.14.0/knowledge-base/why-am-i-unable-to-connect-to-metadefender-optical-diode-with-th#resolution-steps)

1. **Manually configure the laptop’s network settings:**

   - Open **Control Panel** on your Windows device.
   - Navigate to: `Network and Internet` → `Network and Sharing Center` → `Change adapter settings`
   - Right-click on your **active Ethernet adapter** and select **Properties**.
   - Double-click **Internet Protocol Version 4 (TCP/IPv4)**.
   - Select **"Use the following IP address"** and configure:

     - **IP address:** `10.10.10.X` (replace X with any number between 2 and 254, except 10)
     - **Subnet mask:** `255.255.255.0`
     - **Default gateway:** Leave blank (not required)
   - Click **OK** to apply the settings.
2. **Use a straight-through Ethernet cable** to connect the laptop directly to the Netwall device.
3. **Access the Netwall interface:**

   - Open a browser and navigate to: `https://10.10.10.10`
   - Accept any security warnings (self-signed certificate)

---

### [Notes:](/docs/netwalldiode/v1.14.0/knowledge-base/why-am-i-unable-to-connect-to-metadefender-optical-diode-with-th#notes)

- Do **not** use a crossover cable; modern NICs auto-negotiate and a straight-through cable is sufficient.
- Ensure other network interfaces (e.g., Wi-Fi) are disabled to avoid routing conflicts during the connection

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

MetaDefender

<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/knowledge-bases/how-do-i-troubleshoot-network-connectivity-to-metadefender-secur -->

# How do I Troubleshoot Network Connectivity to MetaDefender Security Gateway?

This article applies to all version of MetaDefender Security Gateway

The user was unable to connect to the MetaDefender Security Gateway using a laptop. Attempts to connect failed across multiple machines, browsers, and Ethernet cables. There was uncertainty regarding cable type (crossover vs. straight-through) and proper network configuration, including the correct subnet mask.

**Root Cause:** Incorrect network configuration on the laptop prevented proper communication with the MetaDefender Security Gateway device.

### [**Resolution Steps:**](/docs/netwall/v5.13.2/knowledge-bases/how-do-i-troubleshoot-network-connectivity-to-metadefender-secur#resolution-steps)

Follow these steps to manually configure the network settings and establish a connection:

1. **Open Network Settings**

   - Go to **Control Panel** > **Network and Internet** > **Network and Sharing Center**.
   - Click **Change adapter settings** on the left panel.
2. **Modify Adapter Properties**

   - Right-click the active Ethernet connection and select **Properties**.
   - Double-click **Internet Protocol Version 4 (TCP/IPv4)**.
3. **Assign a Static IP Address**

   - Select **Use the following IP address**.
   - Input an IP address in the same subnet as the MetaDefender Security Gateway (e.g., `10.10.10.X`, where `X` ≠ `10`).
   - Set the **Subnet Mask** to `255.255.255.0`.
   - Leave the **Default Gateway** blank or use `10.10.10.10` if required by your setup.
4. **Save and Close**

   - Click **OK** to apply the settings, then close all dialog boxes.
5. **Connect Using a Standard Ethernet Cable**

   - Use a **straight-through Ethernet cable** to connect the laptop directly to the MetaDefender Security Gateway device.
6. **Access the Web Interface**

   - Open a browser and navigate to: `https://10.10.10.10`
   - Ensure your browser supports secure connections and allows exceptions for self-signed certificates if prompted.

If the issue persists after completing these steps, verify there are no local firewalls or antivirus software blocking the connection.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

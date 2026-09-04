<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/settings/network-discovery -->

# Network & Discovery

Discovery settings is accessible under **Settings --> Network & Discovery.**

### **Network & Discovery settings**

Under this section, you can see all the NICs of MetaDefender OT Security machines, each in a different numbered card.

This information of the NICs matches the NICs settings in the setup wizard that you have completed.

Information of a network interface card includes:

- MAC.
- IP address.
- Netmask.
- Default gateway.
- Used this interface for internet.
- Option for passive scanning.
- Option for active scanning.
- Range of discovery network.

If you need to adjust the method of Host configuration, set it to automatic (DHCP) or Manual, set Address, Netmask, Gateway, set DNS and other fields, click the Edit icon in the right corner of the card. Your changes will be applied to the system after saving.

It should be noted that:

- You can only configure IPs for selected NICs to use as Active Discovery, Online Update, and Manage (Web access).
- Particularly for the NICs used as Passive Discovery, you do not need to configure the IP.
- With “Filter traffic by passive discovery” option, this filter-down traffic is applied for all interfaces. If this field is empty, MetaDefender OT Security will scan all possible traffics from NICs with passive discovery.

*Note*: User don’t need to configure route for NICs, MetaDefender OT Security will handle that.

### How to configure Discovery settings for best performance by MetaDefender OT Security

MetaDefender OT Security machines should have a network card connected to the mirror port and a network card connected to the normal port on the switch to work most effectively.

The NIC connect to mirror port allows us to capture all traffic in the network.

And the NIC that connect to normal port allows MetaDefender OT Security to collect basic profile information such as device name, IP address and more detailed configuration information such as model, firmware versions, installed software/versions and operating system patch levels.

***Set up on Discovery Setting***

1. Ensure the “Connect to SPAN (mirror) port” is selected with a NIC.
2. Select NIC for Online update.
3. Select NIC for Management.
4. Input IP ranges for “Filter traffic by passive discovery”
5. On the NIC(s) that connects to the mirror port, check on “Use this interface for passive discovery”. (Passive Scanning)
6. On the NIC(s) that connects to the normal port, check on “Use this interface for smart active discovery”. (Active Scanning)
7. On the NIC(s) that are not used or not connected to any port, please disable and don’t check any scanning option for those NICs.

*Note:* In case of any discovery settings changes, you need to click on the Save button so that the changes can be applied. Click on the refresh button can get the latest NIC status.

***Test Configuration***

After saving all the changes, you can test the configuration by clicking on the “Test Configuration“ button. A testing coverage will appear when the testing process is completed.

## Wi-Fi Setting

Clicking on the button settings to open the popup Wi-Fi setting.

******Note: Just only focus on the popup Wi-Fi settings until it is closed. Make sure don't impact anything other than it.***

Clicking on the toggle to enable Wi-fi. Then select your Wi-Fi network from the list in “Visible Networks”. In this example, the Wi-Fi we want to connect to is called “Guest_Phone_ BYOD_Only”.

After selecting your Wi-Fi network, if your network requires a password to connect to, you will be prompted to enter it. Then select Connect.

Make sure Wi-Fi is connected. *Do not zoom out on the popup*, just click “X” to close it.

Finally, the wifi is configured.

******Note:***

- *Setting Wifi is not allowed when MetaDefender OT Security is on Web platform. Please switch to desktop before setting Wifi.*
- If you want to use Wifi as management (web access), please be careful that IP address for Web may be changed by DHCP and make sure that the devices under Wifi network is reachable.
- After configuring Wifi, please click on Refresh button to get the latest NIC status.

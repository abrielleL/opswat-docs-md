<!-- source: https://www.opswat.com/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser -->

# Connecting to the Fend Data Diode via Web Browser (Windows, MacOS and Linux)

To configure the diode, you must open a connection with the diode. This section describes how to open a configuration session over ethernet and provides some tips on things to confirm before trying to connect.

## [Step 1: Confirm Your Computer’s Network Settings before Connecting to a Data Diode](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#step-1-confirm-your-computers-network-settings-before-connecting-to-a-data-diode)

The default IP address of a new diode is provided on the Diode Quick Start Guide included with the diode (typically 192.168.1.99). The computer you’re using to connect to the diode will need to be on the same subnet as the diode to successfully connect. For complex networks or ones controlled by an IT department, contact your support team for assistance connecting to a device outside your subnet. For simple networks such as a computer connecting directly to the diode, see below to verify you have the correct network settings. NOTE: Changing network settings on your Windows machine requires administrator privileges.

### [Windows Subnet Setup Instructions](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#windows-subnet-setup-instructions)

#### [Check your current system IP (Windows):](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#check-your-current-system-ip-windows)

1. Open Command Prompt by going to the start menu and typing “CMD” and pressing enter
2. Type “ipconfig”, then press enter
3. Look for an “Ethernet” device similar to below and verify that your IP is similar to 192.168.1.XXX.

#### [If you need to change your IP/subnet (Windows):](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#if-you-need-to-change-your-ipsubnet-windows)

1. In the start menu, type “Control Panel” and open.
2. Click “Network and Internet”, then “Network Sharing Center”, on the left click “Change Adapter Settings”
3. Double click the ethernet device found in the previous section
4. In the new window, click Properties (this requires Admin Privileges on your computer)

5. Double click on “Internet Protocol Version 4”

6. Select the option “Use the following IP address” and enter an IP in the following format (The number in green can be any number you wish higher than 1):

7. The value right below, “Subnet Mask”, will auto-populate so no need to worry about this entry.

### [Linux Subnet Setup Instructions](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#linux-subnet-setup-instructions)

*Depending on your distribution, the steps for viewing and changing your IP address may vary. If your system has a desktop, the instructions below are likely to work.*

#### [Check your current system IP (Linux):](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#check-your-current-system-ip-linux)

1. Open the settings menu from your desktop and select the Network option.
2. Under the “Wired” section (or similar), press the gear icon, and select the option for “IPv4”
3. You should now be able to see the IP address settings for this interface. Make sure the given address is similar to 192.168.1.XXX.

#### [If you need to change your IP/subnet (Linux):](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#if-you-need-to-change-your-ipsubnet-linux)

1. In the menu as described above, make sure the IPv4 method is set to “Manual.”
2. Enter the desired address below in the address box, the subnet in the netmask box, and the gateway in the gateway box.
3. For the subnet, we recommend /24 or 255.255.255.0 (both of these values are the same but expressed in different formats). For the gateway, if the Fend Data Diode is directly connected to the machine, you can enter 192.168.1.1.
4. Press “Apply” to save these settings.

### [Mac Subnet Setup Instructions](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#mac-subnet-setup-instructions)

**Depending on your system, you may need a USB-C to Ethernet adapter to connect a MacBook to your Fend Data Diode. These instructions were written for this case, but they should be applicable to any macOS system.*

#### [Check your current system IP (Mac):](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#check-your-current-system-ip-mac)

1. On the top left-hand corner of your desktop, press the Apple logo and a drop-down menu will appear.

2. Press “System Settings…” and select the Network tab on the left-hand side of the System Settings window.
3. In this menu, look for a network device or service that corresponds to your system’s Ethernet port. In our case, we’re using a USB adapter named “USB 10/100/1000 LAN.”

4. Select the device/service and press “Details…”

5. On the left-hand side of the settings window for the device/service, select “TCP/IP.”

6. You should now see the given IPv4 settings for your Ethernet interface, including the IP address. Make sure the given address is similar to 192.168.1.XXX.
7. If not, continue following the instructions below to change the IP address.

#### [If you need to change your IP/subnet (Mac):](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#if-you-need-to-change-your-ipsubnet-mac)

1. In the settings window as described above, make sure ‘Configure IPv4’ is set to “Manually.”
2. Enter the desired IP address below in the address box, the subnet in the netmask box, and the gateway in the router box.
3. For the subnet, we recommend 255.255.255.0. For the router settings, if the Fend Data Diode is directly connected to the machine, you can enter 192.168.1.1.
4. Press “OK” and the settings will be applied. Depending on your system configuration, you may need to enter administrator credentials to confirm these changes.

## [Step 2: Open the Connection Between Your Computer’s Web Browser and Fend](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#step-2-open-the-connection-between-your-computers-web-browser-and-fend)

Data Diode over Ethernet

1. Confirm that the diode is powered on and that the input side of the diode and the computer are on the same network. Alternatively, a single RJ-45 Ethernet cable can be plugged directly from the Ethernet jack on the computer to the Ethernet jack on the input side of the diode. The single cable connection will work with either a straight-through or crossover RJ45 cable.
2. Open a web browser and enter the data diode’s IP address (found on the Diode Quick Guide) into the search bar.
3. When you first connect to the diode, a warning like the one shown below will appear. The exact language will vary by web browser. This warning appears because the certificate the data diode uses to encrypt its communications isn’t recognized by default in the web browser. To bypass this message and proceed, press “Advanced” then “Proceed to 192.168.1.99 (unsafe)” as shown below:

## [Step 3: Log In and Enter Diode Configuration Mode](/docs/fenddiode/configuring-a-data-diode/connecting-to-the-fend-data-diode-via-web-browser#step-3-log-in-and-enter-diode-configuration-mode)

Now that your browser has been configured to recognize the data diode’s IP address, the Fend Data Diode configuration login page should be visible. Your default login credentials are “user” for the username and the password is printed on the included Diode Quick Start Guide.

Once the password has been successfully entered, the diode will be unlocked in configuration mode for **30 minutes**. The current settings will populate with values from the diode and a timer will appear next to the connection button, showing the time remaining in configuration mode. The configuration session will end either when you close the connection or when the 30-minute session timer expires.

**Note:** **Entering a configuration session with the Fend Diode Configuration Tool will disable all running applications on the diode.** To return to operational mode once configuration has been completed, you must click either the “Save & Exit” or “Exit Without Saving” buttons in the upper right-hand corner of the configuration interface. Either button closes the configuration session and tells the diode to reboot into operational mode. For your changes to be saved after the reboot you must click the “Save & Exit” button.

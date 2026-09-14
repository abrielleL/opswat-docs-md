<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application -->

# Initial configuration for Site Manager & Network Sensor - Bundle 2 in 1 on local management console application

## [About this task](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#about-this-task)

Use this procedure for Site Manager & Network Sensor - Bundle 2 in 1 Configuration Login and Network Configuration for the Site Manager & Network Sensor - Bundle 2 in 1 on the local management console application

## [Before you begin](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#before-you-begin)

- Ensure that you completed the installation for the Site Manager & Network Sensor - Bundle 2 in 1 on the local management console application.

Prepare display screen, keyboard and mouse physically attached to the Site Manager & Network Sensor - Bundle 2 in 1 server to serve during the configuration process

## [Procedure](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#procedure)

After installation, the MetaDefender OT Security Site Manager & Network Sensor - Bundle 2 in 1 on local management console application is starting

## [Site Manager & Network Sensor - Bundle 2 in 1 Configuration Login](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#site-manager--network-sensor---bundle-2-in-1-configuration-login)

### [1. Login with the default username/password](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#1-login-with-the-default-usernamepassword)

Steps:

1. Input username and password for the admin default user
2. Click Login

Login with the default credentials

### [2. Reset the password on the first login](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#2-reset-the-password-on-the-first-login)

After successfully logging in with the default username and password, it is necessary to reset the password. Steps:

1. Input new password
2. Input to confirm new password
3. Click Submit

Reset Password

## [Site Manager & Network Sensor - Bundle 2 in 1 Network Settings](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#site-manager--network-sensor---bundle-2-in-1-network-settings)

Overview Site Manager & Network Sensor - Bundle 2 in 1 Network Settings

### [1. Checking Network Interface](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#1-checking-network-interface)

During this step, our application will detect the Network Interface Cards (NICs) that are currently plugged into your computer. This allows our application to determine which NICs are available for use with our software.

If you have multiple NICs connected to your computer (such as a Built-in NIC, USB NIC 1, and USB NIC 2), our application will display all available NICs on the screen. To help you identify which port each NIC is connected to, you can unplug the cable and the status of the NIC will be changed to "Unavailable" in our application.

If our application fails to detect all of your available NICs, you can click the "**Recheck**" button in the top right corner of the screen to rescan for all NICs.

Recheck button

To use an NIC with our software, toggle the button next to its name. You can disable NICs you don't want to use.

Enable/Disable Network Interface

Click on the **Save** button to save the changes.

### [2. Select NIC using for Enterprise Connectivity and scanning](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#2-select-nic-using-for-enterprise-connectivity-and-scanning)

#### [**2.1. Select NIC using for Enterprise connectivity**](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#21-select-nic-using-for-enterprise-connectivity)

The purpose of this is to select a specific NIC for connecting between the Site Manager & Network Sensor - Bundle 2 in 1 and the Enterprise.

Click “**Select a NIC**” under “**Using for Enterprise Connectivity**” to choose a specific NIC from the droplist.

This list displays all the NICs we enabled earlier, and we only need to select one.

Select NIC using for Enterprise Connectivity

#### [**2.2. Select NIC using for scanning**](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#22-select-nic-using-for-scanning)

You can set up discovery settings for each NIC by selecting either "**Passive discovery**" or "**Smart active discovery**". The system will do the scanning based on the network configuration for NICs that you set up (for both active and passive scanning). Particularly:

- **Passive discovery**: This setting allows the NIC to receive packets from Switch. This is useful for monitoring network traffic without disrupting it. Passive discovery requires the selected NIC to be connected to the SPAN (mirror) port of the switch. We recommend the users use built-in NIC for passive scanning to have better performance.

Select NIC for Passive Discovery

- **Smart active discovery**: This setting sends packets to probe the network and discover other devices. This is useful for identifying network topology and detecting potential issues. The NIC for Smart active discovery is recommended NOT to be connected to the SPAN (mirror) port of the switch.

Select NIC for Active Discovery

### [3. Select NIC using for External Sensor Connectivity](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#3-select-nic-using-for-external-sensor-connectivity)

The purpose of this is to select a specific NIC for connecting between the Site Manager & Network Sensor - Bundle 2 in 1 and the Sensor.

Click “**Select a NIC**” under “**Using for Enxternal Sensor Connectivity**” to choose a specific NIC from the droplist.

This list displays all the NICs we enabled earlier, and we only need to select one.

Select NIC using for Sensor Connectivity

### [4. Select NIC using for Patch Management](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#4-select-nic-using-for-patch-management)

This aims to select a specific NIC for Integrated patching capabilities for firmware from Siemens vendor to streamline updates and manage vulnerabilities.

Click “**Select a NIC**” under “**Using for Patch Management**” to choose a specific NIC from the droplist. This list displays all the NICs we enabled earlier, and we only need to select one.

Select NIC using for Patch Management

### [5. Configure Network Interfaces](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#5-configure-network-interfaces)

In this step, you can access and configure a list of available network interfaces (NICs). To configure a NIC, click on the “**Edit**” button to access the configuration options of the NIC selected in the previous step.

Click on the “**Edit**” button to access the configuration options

By default, the option is **Auto (DHCP),** In case your system has a DHCP server, just enter additional DNS.

Then click the **Apply** button to save the changes.

Config Auto(DHCP) for NIC

For optimal performance, it is recommended to use static IP addresses. Therefore, we should switch to **Manual** configuration.

Config Manual for NIC

Please enter the required details - your address, netmask, gateway, and DNS, in the provided fields. After entering all the details, click on the "**Apply**" button to save the changes.

Finally, save your configuration, simply click on the **Save** button located at the top right corner of the screen.

Click on the **Save** button to save the configuration

## [Network Connectivity - Site Manager & Network Sensor - Bundle 2 in 1 and Enterprise Manager/NetworkSensor communication](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#network-connectivity---site-manager--network-sensor---bundle-2-in-1-and-enterprise-managernetworksensor-communication)

Based on your organization's security rules, it's important to select the appropriate communication method for MetaDefender OT Security when setting up connectivity between the Site Manager & Network Sensor - Bundle 2 in 1 and the Enterprise Manager or Network Sensors.

*Note: Make sure to select the matching communication model between all components involved: Site Manager & Network Sensor - Bundle 2 in 1, Enterprise Manager, and Network Sensors. This ensures consistent and reliable communication across the system.

### [1. Site Manager & Network Sensor - Bundle 2 in 1 and Network Sensor communication](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#1-site-manager--network-sensor---bundle-2-in-1-and-network-sensor-communication)

- **Model #1. Bi-directional (from Sensor to Site and vice versa)**

Two-way (inbound + outbound) communications between components

- **Model #2. Uni-directional (only from Sensor to Site)**

One-way (outbound) communication to the upper component.

### [2. Site Manager & Network Sensor - Bundle 2 in 1 and Enterprise Manager communication](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#2-site-manager--network-sensor---bundle-2-in-1-and-enterprise-manager-communication)

- **Model #1. Bi-directional (from Site to Enterprise and vice versa)**

Two-way (inbound + outbound) communications between components

- **Model #2. Uni-directional (only from Site to Enterprise)**

One-way (outbound) communication to the upper component.

When selecting this communication method, you'll need to:

1. **Input the Enterprise Manager IPv4 Address**: Enter the IP address of the Enterprise Manager to establish the connection.
2. **Input the Current Site Name**: Provide the name of the site that corresponds to the Site Manager & Network Sensor - Bundle 2 in 1.
3. **Save and Establish Connection**: Once you've entered the required information, click on **Save and Establish Connection**. This action will save the configuration and add the Site Manager & Network Sensor - Bundle 2 in 1 to the Enterprise Manager system.

## [Time Settings](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#time-settings)

Configuring the system time can be done using two methods: manual time setting and synchronizing time via an NTP (Network Time Protocol) server. You can choose the most suitable option based on your system’s requirements.

### [**1. Manual Time Setting**](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#1-manual-time-setting)

In this method, users can manually set the system's time and select the appropriate timezone.

Steps to Configure Time Manually:

**Click to Select Manual**

**Select Timezone:**

- Look for the Timezone dropdown or field.
- Choose your desired time zone from the list of available options. For example, you can select *Asia/ Ho Chi Minh*, etc.

- Once you’ve entered the correct timezone, click on the **Apply** button to store your changes.

**Manually Set the Date and Time** **if it is not correct.**

Click on “Click here” to open the Change system Time popup:

Then click “Add system time”:

In the **Date** and **Time** fields, manually input the current date and time.

- **Date Format**: Typically follows YYYY-MM-DD (e.g., 2024-08-29).
- **Time Format**: The time format follows the pattern HH:MM:SS (e.g., 11:01:19) using the 24-hour clock format.

**Save the Settings**: Once you’ve entered the correct date, time, and timezone, click on the **Save** button to store your changes.

**Verify the Changes**: Ensure that the system reflects the correct date, time, and timezone on the interface.

### [**2. NTP Servers**](/docs/md-ot-security/v.3.4.0/configuration/initial-configuration-for-mdots-site-bundle-on-local-application#2-ntp-servers)

NTP (Network Time Protocol) is a protocol designed to synchronize the clocks of networked devices to a global standard time, usually via online servers. This method ensures that the system time is accurate and automatically updated.

Steps to Configure NTP Server:

**Click to select NTP Servers**:

**Input NTP Server Address**:

You will be prompted to input an NTP server. Examples of commonly used NTP servers are:

- pool.ntp.org
- time.google.com
- time.windows.com

Enter the preferred NTP server URL or IP address into the **NTP Server** field.

**Apply the Settings**:

After entering the NTP server information, click the **Save** button to store the settings.

The system will now synchronize its time with the NTP server at regular intervals.

**Verify NTP Synchronization**:

Check the system time to ensure it matches the correct time after synchronization.

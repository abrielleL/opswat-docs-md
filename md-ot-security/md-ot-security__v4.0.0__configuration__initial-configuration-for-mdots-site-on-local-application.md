<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application -->

# Initial configuration for Site Manager on local management console application

## [About this task](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#about-this-task)

Use this procedure for Site Manager Configuration Login and Network Configuration for the Site Manager on the local management console application.

## [Before you begin](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#before-you-begin)

Ensure that you have completed the installation of the Site Manager on the local management console application.

Prepare the display screen, keyboard, and mouse physically attached to the Site Manager server to serve during the configuration process.

## [Procedure](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#procedure)

After installation, the MetaDefender OT Security Site Manager on the local management console application starts.

## [Site Manager Configuration Login](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#site-manager-configuration-login)

### [1. Login with the default username/password](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#1-login-with-the-default-usernamepassword)

Steps:

1. Input username and password for the admin default user
2. Click Login

Log in with the default credentials

### [2. Reset the password on the first login](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#2-reset-the-password-on-the-first-login)

After successfully logging in with the default username and password, it is necessary to reset the password:

1. Input new password
2. Input to confirm new password
3. Click **Submit** button

Reset password

## [Site Manager (Aggregator) Info](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#site-manager-aggregator-info)

In this step, the user will name the Site Manager (Aggregator).

After inputting the name, click **Save and Continue** to go to the next step.

## [Site Manager Network Settings](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#site-manager-network-settings)

Overview Site Manager Network Settings

### [1. Checking Network Interface](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#1-checking-network-interface)

During this step, our application will detect the Network Interface Cards (NICs) that are currently plugged into your computer. This allows our application to determine which NICs are available for use with our software.

If you have multiple NICs connected to your computer (such as a Built-in NIC, USB NIC 1, and USB NIC 2), our application will display all available NICs on the screen. To help you identify which port each NIC is connected to, you can unplug the cable and the status of the NIC will be changed to **Unavailable** in our application.

If our application fails to detect all of your available NICs, you can click the **Recheck** button in the top right corner of the screen to rescan for all NICs.

Recheck button

To use an NIC with our software, toggle the button next to its name. You can disable NICs you don't want to use.

Enable/Disable Network Interface

Click on the **Save** button to save the changes.

### [2. Select NIC for Enterprise Connectivity](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#2-select-nic-for-enterprise-connectivity)

The purpose of this is to select a specific NIC for connecting between the Site Manager and the Enterprise.

Click **Select a NIC** under **Using for Enterprise Connectivity** to choose a specific NIC from the drop-down list.

This list displays all the NICs we enabled earlier, and we only need to select one.

Select NIC for Enterprise Connectivity

### [3. Select NIC for Sensor Connectivity](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#3-select-nic-for-sensor-connectivity)

The purpose of this is to select a specific NIC for connecting between the Site Manager and the Sensor.

Click **Select a NIC** under **Using for Sensor Connectivity** to choose a specific NIC from the drop-down list.

This list displays all the NICs we enabled earlier, and we only need to select one.

Select NIC for Sensor Connectivity

### [4. Configure Network Interfaces](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#4-configure-network-interfaces)

In this step, you can access and configure a list of available network interfaces (NICs). To configure a NIC, click on the **Edit** button to access the configuration options of the NIC selected in the previous steps.

Click on the **Edit** button to access the configuration options.

By default, the option is **Auto (DHCP),** In case your system has a DHCP server, just enter additional DNS.

Then click the **Apply** button to save the changes.

Config Auto(DHCP) for NIC

For optimal performance, it is recommended to use static IP addresses. Therefore, we should switch to **Manual** configuration.

Config Manual for NIC

Please enter the required details - your address, netmask, gateway, and DNS, in the provided fields. After entering all the details, click on the **Apply** button to save the changes.

Finally, save your configuration, simply clicking on the **Save and Continue.**

Click on the **Save and Continue** button to save the configuration

## [SSH Access Management](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#ssh-access-management)

At this step, we can manage SSH access rights by adding IPs to the allowed list and adding a password if needed.

## [Network Connectivity - Site Manager and Enterprise Manager/Network Sensor communication](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#network-connectivity---site-manager-and-enterprise-managernetwork-sensor-communication)

Based on your organization's security rules, it's important to select the appropriate communication method for MetaDefender OT Security when setting up connectivity between the Site Manager and the Enterprise Manager or Network Sensors.

***Note:*** *Make sure to select the matching communication model between all components involved: Site Manager, Enterprise Manager, and Network Sensors. This ensures consistent and reliable communication across the system.*

### [1. Site Manager and Network Sensor communication](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#1-site-manager-and-network-sensor-communication)

- **Model #1: Site Manager and Network Sensor communication**

- **Model #2:** **Use Enterprise Manager Console to enroll Network Sensor to this Site Manager**

### [2. Site Manager and Enterprise Manager communication](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#2-site-manager-and-enterprise-manager-communication)

- **Model #1:** **Enter the IPv4 Address of Enterprise Manager**

When selecting this communication method, you'll need to:

1. **Input the Enterprise Manager IPv4 Address**: Enter the IP address of the Enterprise Manager to establish the connection.
2. **Establish Connection**: Once you've entered the required information, click on **Establish Connection**. This action will save the configuration and add the Site Manager to the Enterprise Manager system.

- **Model #2:** **Use Enterprise Manager Console to enroll this Site Manager to Enterprise Manager**

## [Time Settings](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#time-settings)

Configuring the system time can be done using two methods: manual time setting and synchronizing time via an NTP (Network Time Protocol) server. You can choose the most suitable option based on your system’s requirements.

### [**1. Manual setting for Time Settings**](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#1-manual-setting-for-time-settings)

In this method, users can manually set the system's time and select the appropriate time zone.

**Steps to configure time settings manually:**

**Step 1** - Select option **Manual**

**Step 2** - Click **Select timezone*** to open drop-down list:

- Choose your desired time zone from the list of available options. For example, you can select ***Asia/ Ho Chi Minh***, etc.
- Once you’ve entered the correct time zone, click on the **Apply** button to store your changes.

Select time zone

**Step to manually set the Date and Time if it is not correct:**

**Step 1** - Click the **Click here** button to open the change system time popup:

**Step 2** - Click **Add system time:**

In the **Date** and **Time** fields, manually input the current date and time:

- **Date Format**: Typically follows YYYY-MM-DD (e.g., 2024-08-29).
- **Time Format**: The time format follows the pattern HH:MM:SS (e.g., 11:01:19) using the 24-hour clock format.

**Step 4** - Save the settings:

Once you’ve entered the correct date, time, and time zone, click on the **Save** button to store your changes.

**Step 5** - Verify the changes:

Ensure that the system reflects the correct date, time, and time zone on the interface.

### [**2. NTP Servers**](/docs/md-ot-security/v4.0.0/configuration/initial-configuration-for-mdots-site-on-local-application#2-ntp-servers)

NTP (Network Time Protocol) is a protocol designed to synchronize the clocks of networked devices to a global standard time, usually via online servers. This method ensures that the system time is accurate and automatically updated.

**Steps to configure NTP Servers**

**Step 1** - Select option **NTP Servers**

**Step 2** - Click on **NTP Servers** to add NTP Server:

**Step 3** - Input **NTP Server Address:**

You will be prompted to input an NTP server. Examples of commonly used NTP servers are:

- pool.ntp.org
- time.google.com
- time.windows.com

Enter the preferred NTP server URL or IP address into the **NTP Server** field.

**Step 4** - Apply the Settings:

After entering the NTP server information, click the **Save** button to store the settings. The system will now synchronize its time with the NTP server at regular intervals.

**Step 5** - Verify NTP Synchronization:

Check the system time to ensure it matches the correct time after synchronization.

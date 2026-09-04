<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/operating/smart-asset-profiling -->

# Smart Asset Profiling

## [Overview](/docs/md-ot-security/v.3.4.0/operating/smart-asset-profiling#overview)

The smart asset profiling tab is accessible under **Assets → Smart Asset Profiling.**

This page lists all protocols available for smart profiling scanning and its history.

Table include:

- Information of profile: Profile name, Information icon, Protocol, Number of devices supported, Number of devices supported, Number of devices to be scanned, Created date, Last run.
- Function buttons for each profile: Run, Edit, and History.
- Checkbox for each profile and Select All checkbox.

## [Main features](/docs/md-ot-security/v.3.4.0/operating/smart-asset-profiling#main-features)

### [Edit Profile](/docs/md-ot-security/v.3.4.0/operating/smart-asset-profiling#edit-profile)

The popup **Edit profile** is accessible under **Assets → Smart Asset Profiling → Edit.**

The popup **Edit profile** lists all devices added to scan using the protocol.

Users can add devices automatically (suggested by MD OT Security) or manually (select from the list).

The **Add device** popup allows the user to filter, select one or many devices, and add them to the profile.

Back to the **Edit profile** popup, the device table includes some device common information fields such as name, type, and IP.

In addition, the user can choose a device to scan, remove a device from the table, and decide the priority of the profile for a device, in case two or more profiles scan the device.

There are two options for the scan result for the user to choose:

- Auto overwrite: MetaDefender OT Security will automatically apply new information scanned by the profile to the device.
- Wait for confirmation: MetaDefender OT Security will list new information scanned to the **Review property changes** popup and show it to the user for confirmation.

Finally, the user can choose to Save, Save & Run, or cancel the change.

### [Run profile](/docs/md-ot-security/v.3.4.0/operating/smart-asset-profiling#run-profile)

User can choose to run smart profiling individually or simultaneously by clicking the "Run" button or checking checkboxes and using the "Run selected profiles" button.

While the profiling process is running, users are unable to run other profile.

Ensure your industrial devices have opened the relevant ports for scanning. Here is a list of ports that need to be opened to use Smart Asset Profiling

| **Profile** | **The Industrial Device Protocol/Port needs to open** |
| --- | --- |
| ABB profile | HTTP:80 |
| BACnet/IP profile | UDP:47808 |
| B&R Industrial Automation profile | HTTP:80 |
| Emerson (GE-SRTP) profile | UDP:18245 |
| Emerson (HTTP) profile | HTTP:80 |
| EtherNet/IP profile | TCP:44818 |
| Mitsubishi profile | TCP:5562 |
| Modbus-TCP profile | TCP:502 |
| PROFINET IO (DCE/RPC) profile | UDP:34964 |
| S7COMM-PLUS profile - Extended | TCP:102 |
| S7COMM profile | TCP:102 |
| SNMP profile | UDP:161 |

#### [Review property changes](/docs/md-ot-security/v.3.4.0/operating/smart-asset-profiling#review-property-changes)

After the profiling process finished, if there is any change detected, the review property changes popup will appear. The popup can still be opened through the button "Review property changes" on the main page.

Users can see the common information of device that is detected with property changes here as the image above.

Furthermore, the user can view and decide what property to change at the **New detected properties** popup through the "Eye" button.

Users can view all property changes detected here and can decide to accept or ignore each change individually.

### [Profile History](/docs/md-ot-security/v.3.4.0/operating/smart-asset-profiling#profile-history)

Lastly, all change activities are recorded and can be viewed through the history button of each profile.

### [Detect the configuration and security status of Siemens PLC devices](/docs/md-ot-security/v.3.4.0/operating/smart-asset-profiling#detect-the-configuration-and-security-status-of-siemens-plc-devices)

**MD OT Security** can scan Siemens Programmable Logic Controllers (PLCs) using **S7COMM - Extended** profile to detect their configuration settings and assess the **security status**. By conducting a comprehensive scan, it retrieves detailed information about the device’s current setup

- **Failsafe:** Based on its ArticleNumber, is this a failsafe device?
- **Firmware Update Allowed:** Is a firmware update possible for this device?
- **Slot:** number for the hardware item
- **Slot Name:** This property is used in the SIMATIC Automation Tool user interface. It is not relevant for API operations
- **Station Number:** Station number of the device
- **Backup Allowed**: TRUE if this device currently allows Backup
- **Backup Supported**: TRUE if this device supports backup
- **Restore Allowed**: TRUE if this device currently allows restore
- **Restore Supported**: TRUE if this device supports restore
- **Change Mode Allowed**: TRUE if this device currently allows CPU run mode change
- **Change Mode Supported**: TRUE if this device supports CPU run mode change
- **Password Allowed**: TRUE if this device currently allows passwords
- **Password Supported**: TRUE if this device supports passwords
- **Security Supported**: This device supports TLS security and configuration data protection
- **Security Allowed**: This device presently allows TLS security and configuration data protection
- **CPU Protection Level**: The protection level that is set on the CPU, independent of the password. It has the options below:

  - Failsafe
  - Full
  - Read
  - HMI
  - NoAccess
  - NoPassword
- **Operating Mode**: Designates the current mode of the CPU. This value is read-only. It has the options below:

  - Stop
  - Run
- **Password Protection Level**: Protection level of a legitimized CPU password. It has the options below:

  - Failsafe
  - Full
  - Read
  - HMI
  - NoAccess
  - NoPassword
- **Protected**: Is the CPU currently protected? This means a password is required to access some or all features depending on access level.

  - When the CPU is reset to the factory setting or vendor default setting, the value of the Access level is Full access (NoPassword)
  - If the CPU is configured as Read, HMI, and No access then the PLC is password protected.

- **Hostname:** the hostname is also referred to as the "device name" and is critical for network communication.
- **Product LifeCyle Status:** Currently, we support getting this information from Siemens and Rockwell Automation.

  - **Siemens** device we have the options below:

    - **Sales Release:** Marks the point at which a product is officially released for sale. Marketing, sales, and support teams are trained, and materials are available for customer use.
    - **Delivery Release:** Indicates that the product is fully prepared for delivery and deployment. This phase ensures all logistical, technical, and operational requirements are met.
    - **Announcement Phase Out:** This is the stage when Siemens formally communicates the intention to phase out a product. It serves as a transition period for customers to adapt.
    - **Product Cancellation:** The phase when a product is officially removed from the sales portfolio and is no longer available for new orders.
    - **Product Discontinuation:** Marks the official cessation of support, maintenance, and upgrades for the product.
    - **End Of PLM:** This represents the absolute final phase where all product-related lifecycle management activities are terminated.
  - **Rockwell Automation** device we have the options below:

    - **Active:** The product is in full production and widely available for purchase.
    - **Active Mature:** The product is still available for sale but is nearing the end of its active marketing and promotion phase.
    - **Discontinued:** The product is no longer available for new orders and has been officially removed from active sales.
    - **End of Life:** The final phase where all support, updates, and spare parts for the product cease.
    - **Not Set:** The lifecycle status of the product is not yet determined or explicitly defined.

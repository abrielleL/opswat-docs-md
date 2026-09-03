<!-- source: https://www.opswat.com/docs/md-ot-security/operating/discovery-settings -->

# Discovery Settings

## [Overview](/docs/md-ot-security/operating/discovery-settings#overview)

The **Discovery Settings** page allows you to configure device discovery settings and manage BYOD (Bring Your Own Device) in the Neuralyzer system. This page is divided into two main sections: **Define Subnets for BYOD** and **Discovery Processing Settings**.

The **Discovery Settings** tab is accessible under **Assets** → **Discovery Settings.**

*(Image could not be embedded — see Confluence)*

## [Section 1: Define Subnets for BYOD](/docs/md-ot-security/operating/discovery-settings#section-1-define-subnets-for-byod)

### [Purpose](/docs/md-ot-security/operating/discovery-settings#purpose)

This section allows you to define subnets for the system to automatically recognize BYOD devices.

### [Components](/docs/md-ot-security/operating/discovery-settings#components)

#### [1.1 Toggle Switch - Define Subnets for BYOD](/docs/md-ot-security/operating/discovery-settings#11-toggle-switch---define-subnets-for-byod)

- **Location**: Toggle switch at the top of the section
- **Current Status**: ON (blue color)
- **Function**: Enable/disable the subnet definition feature for BYOD

**How to use:**

- Click the toggle to enable/disable the feature
- When ON: The system will use defined subnets to recognize BYOD devices
- When OFF: The system will only use automatic recognition

#### [1.2 Subnet Input Field](/docs/md-ot-security/operating/discovery-settings#12-subnet-input-field)

- **Label**: "Subnets (CIDR format e.g:192.168.1.1/24) *"
- **Format**: CIDR (Classless Inter-Domain Routing)
- **Examples**: `192.168.1.0/24`, `10.0.0.0/8`, `172.16.0.0/16`
- **Required**: Yes (asterisk *)

**How to enter subnets:**

1. Enter the subnet address in CIDR format
2. After entering, press one of the following keys to accept:

   - **Tab**
   - **Enter**
   - **Space**

**Valid examples:**

- `192.168.1.0/24` - Subnet for 192.168.1.x network
- `10.0.0.0/8` - Subnet for 10.x.x.x network
- `172.16.0.0/16` - Subnet for 172.16.x.x network

#### [1.3 Checkbox - Apply for devices with local administered MAC only](/docs/md-ot-security/operating/discovery-settings#13-checkbox---apply-for-devices-with-local-administered-mac-only)

- **Location**: Below the subnet input field
- **Current Status**: Checked (blue checkmark)
- **Function**: Apply settings only to devices with locally administered MAC addresses

**Explanation:**

- **Checked**: Only devices with locally administered MAC addresses will have BYOD settings applied
- **Unchecked**: All devices in the subnet will have BYOD settings applied

#### [1.4 Save Button](/docs/md-ot-security/operating/discovery-settings#14-save-button)

- **Location**: End of the Define Subnets for BYOD section
- **Color**: Blue
- **Function**: Save changes in this section

**How to use:**

1. Configure the desired settings
2. Click the **"Save"** button
3. The system will display a confirmation message

## [Section 2: Discovery Processing Settings](/docs/md-ot-security/operating/discovery-settings#section-2-discovery-processing-settings)

### [Purpose](/docs/md-ot-security/operating/discovery-settings#purpose)

This section allows you to configure how the system processes discovered devices.

### [Components](/docs/md-ot-security/operating/discovery-settings#components)

#### [2.1 Configuration Question](/docs/md-ot-security/operating/discovery-settings#21-configuration-question)

- **Question**: "Assign IPv4 in ARP connection to Router"
- **Purpose**: Decide whether to assign IPv4 addresses in ARP connections to Router

#### [2.2 Radio Buttons](/docs/md-ot-security/operating/discovery-settings#22-radio-buttons)

There are two options to answer the above question:

**"Yes" option:**

- **Status**: Not selected
- **Function**: Assign IPv4 addresses in ARP connections to Router

**"No" option:**

- **Status**: Selected (blue dot)
- **Function**: Do not assign IPv4 addresses in ARP connections to Router

**How to change:**

1. Click on the desired radio button
2. The selection will be updated immediately

#### [2.3 Save Button](/docs/md-ot-security/operating/discovery-settings#23-save-button)

- **Location**: End of the Discovery Processing Settings section
- **Color**: Blue
- **Function**: Save changes in this section

## [Navigation Bar and System Information](/docs/md-ot-security/operating/discovery-settings#navigation-bar-and-system-information)

### [Overview Statistics](/docs/md-ot-security/operating/discovery-settings#overview-statistics)

The navigation bar displays important statistics:

- **Asset List**: 151 (Asset list)
- **Asset Alerts**: 5 (Asset alerts)
- **Misconfigurations**: 0 (Misconfigurations)
- **Vulnerabilities**: 219 (Vulnerabilities)

### [Navigation Tabs](/docs/md-ot-security/operating/discovery-settings#navigation-tabs)

- **Patching Management**: Patch management
- **Update History**: Update history
- **Smart Asset Profiling**: Smart asset profiling
- **Discovery Settings**: Discovery settings (currently selected)

### [Utility Buttons](/docs/md-ot-security/operating/discovery-settings#utility-buttons)

- **Refresh**: Refresh page
- **Search/Filter**: Search and filter
- **User Profile**: User profile

## [Recommended Workflow](/docs/md-ot-security/operating/discovery-settings#recommended-workflow)

### [1. Configure BYOD Subnets](/docs/md-ot-security/operating/discovery-settings#1-configure-byod-subnets)

1. Ensure the "Define Subnets for BYOD" toggle is in ON state
2. Enter CIDR subnets in the input field
3. Decide whether to apply to devices with locally administered MAC addresses
4. Click **Save** to save the settings

### [2. Configure Discovery Processing](/docs/md-ot-security/operating/discovery-settings#2-configure-discovery-processing)

1. Select "Yes" or "No" for the IPv4 assignment in ARP connection question
2. Click **Save** to save the settings

### [3. Verify Settings](/docs/md-ot-security/operating/discovery-settings#3-verify-settings)

1. Review the configured settings
2. Monitor confirmation messages from the system
3. Check device discovery activity in the Asset List

## [Important Notes](/docs/md-ot-security/operating/discovery-settings#important-notes)

### [CIDR Format](/docs/md-ot-security/operating/discovery-settings#cidr-format)

- Use standard CIDR format: `IP_address/subnet_mask`
- Example: `192.168.1.0/24` means subnet from 192.168.1.0 to 192.168.1.255
- Ensure IP address and subnet mask are valid

### [MAC Address Local Administered](/docs/md-ot-security/operating/discovery-settings#mac-address-local-administered)

- Only applies to devices with locally administered MAC addresses
- Helps distinguish between personal and corporate devices

### [Saving Settings](/docs/md-ot-security/operating/discovery-settings#saving-settings)

- Each section has its own Save button
- Need to save each section after making changes
- System will display confirmation message when saved successfully

## [Troubleshooting](/docs/md-ot-security/operating/discovery-settings#troubleshooting)

### [CIDR Format Error](/docs/md-ot-security/operating/discovery-settings#cidr-format-error)

- Check if the input format is correct
- Ensure subnet mask is valid (e.g., /24, /16, /8)

### [Cannot Save Settings](/docs/md-ot-security/operating/discovery-settings#cannot-save-settings)

- Check network connection
- Ensure you have admin privileges to change settings
- Try refreshing the page and re-entering

### [Devices Not Discovered](/docs/md-ot-security/operating/discovery-settings#devices-not-discovered)

- Check if subnets are defined correctly
- Verify devices are within the configured subnet
- Check if BYOD toggle is enabled

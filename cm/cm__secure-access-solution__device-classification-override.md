<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/device-classification-override -->

# Device Classification Override

## Executive Summary

The Device Classification Override feature in MetaDefender NAC empowers network administrators to manually correct device identification inaccuracies, ensuring more precise network access control and security policy enforcement. This feature addresses limitations in automated DHCP fingerprinting by allowing manual assignment of device types (VM, Desktop, Laptop, etc.) and operating system classifications (Windows, macOS, Linux, etc.).

**Key Benefits:**

- Improves accuracy of device identification for agentless devices
- Enhances future automated classification through machine learning
- Reduces false positives in compliance reporting
- Enables granular access control based on accurate device profiles

---

## Prerequisites

Before using the Device Classification Override feature, ensure you have:

### Required Access Permissions

- Administrative access to My OPSWAT Central Management console
- **Inventory Management** permissions

### System Requirements

- MetaDefender NAC Edge VM version 1.9.0 or later
- Device is actively connect to the NAC Network
- Devices must be in "Unknown" compliance status for override capability

## Feature Overview

### Understanding DHCP Fingerprinting vs. Manual Override

MetaDefender NAC primarily relies on **DHCP fingerprinting** for automatic device identification. This process analyzes DHCP requests and network behavior patterns to determine device types and operating systems. However, this automated method has inherent limitations:

- **Accuracy Rate**: Approximately 85-90% under optimal conditions
- **Coverage Gaps**: Some devices may not generate sufficient fingerprinting data
- **False Classifications**: Similar network behaviors can lead to misidentification
- **Unknown Devices information**: Devices information may remain unclassified (N/A) when fingerprinting fails

The **Device Classification Override** feature bridges these gaps by enabling manual intervention while contributing to the system's learning algorithm for improved future accuracy.

### How Override Benefits Future Identification

When administrators perform manual overrides, the system:

1. Stores the correlation between network fingerprint and actual device characteristics
2. Updates machine learning models with verified classification data
3. Improves automatic detection accuracy for similar devices in the future
4. Builds a more comprehensive device profile database

---

## When to Use Override

Use Device Classification Override in the following scenarios:

### Primary Use Cases

- **Unknown Status Devices**: Devices showing "Unknown" compliance status that require policy application
- **Misclassified Devices**: Devices incorrectly identified by automated fingerprinting
- **Critical Asset Identification**: High-value devices requiring precise classification for security policies
- **Compliance Reporting**: Ensuring accurate device counts for audit and compliance purposes

### Decision Criteria

Consider override when:

- Device behavior doesn't match current classification
- Security policies aren't applying correctly due to misidentification
- Device appears in "Unknown" status for more than 24 hours
- Manual verification confirms automated classification is incorrect

### When NOT to Use Override

- Devices are correctly classified and compliant
- Uncertainty exists about the actual device type or OS
- Override would conflict with established network security policies

---

## Override Classification Step-by-Step Procedures

### Accessing Device Classification Override

1. **Go to Devices Inventory**
   1. Navigate to `My OPSWAT Central Management → Inventory → Devices`
2. **Devices status**

The Devices page displays three compliance statuses:

- **Compliant**: Information reported from MetaDefender Endpoint that devices meeting all policy requirements
- **Non-compliant**: Information reported from MetaDefender Endpoint that devices violating one or more policies
- **Unknown**: Devices do not have Agent installed

> **Info**
>
> Only devices with Unknown status can be overridden. This restriction prevents modification of correctly classified devices reported from MetaDefender Endpoint

### Performing Device Classification Override

3. **Select Target Device**

- Locate the device requiring classification override
- Click the checkbox next to the device entry
- Ensure its status is “Unknown”

4. **Open Override Panel**

- Click the **Select Action** dropdown menu
- Choose **Override Classification** from the available options

5. **Configure New Classification**

The **Override Classification** dialog will display with the following options:

**Device Type Selection**:

- Choose the appropriate device type from the dropdown
- See [Available Classifications](#available-classifications) for complete options

**OS Type Selection**:

- Select the correct operating system
- Ensure accuracy as this affects security policy application

**Notes Field** (Optional but Recommended):

- Document the reason for override
- Include verification method (e.g., "Confirmed via physical inspection")
- Add any relevant details for future reference

6. **Apply and Confirm Changes**

- Review all selections for accuracy
- Click **Save** to confirm the classification override
- The system will immediately update the device profile and apply relevant policies

### Post-Override Verification

7. **Verify Classification Update**

- Refresh the device inventory view
- Confirm the device now shows correct classification

> **Info**
>
> A tooltip icon will appear next to the new data. Hover to view original classification data.

---

### Revert an Override Classification

> **Info**
>
> If the information provided during the admin override is incorrect, you have a Revert option in the Override Classification popup to restore the original classification values:
>
> 1. Follow steps 1–4 to reopen the override dialog
> 2. Click on Revert button
> 3. Confirm to restore original device info

### Bulk action

To Override/Revert Classification for multiple devices:

1. Select multiple checkboxes in the **Devices** list
2. Ensure all selected devices are Unknown
3. Perform override/revert using the same steps

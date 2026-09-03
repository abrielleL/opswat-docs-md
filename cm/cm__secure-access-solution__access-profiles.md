<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/access-profiles -->

# Access Profiles

The Access Profiles feature allows administrators to define VLAN assignments or other access controls for devices connecting to the network. Access Profiles are assigned to devices based on rules that match their group membership and compliance status.

To create Access Profiles,

1. Log into the **My OPSWAT Central Management** console as an administrator
2. Navigate to **RADIUS NAC**
3. Click on **Access Profiles** tab
4. Click **Add Profile** button to add new Profile
   - Provide detailed information:
     - Name: Name of the Access Profiles, for example: “Compliance Staff”
     - Select Vendors to applied to the Access Profile

![](https://uploads.developerhub.io/prod/6Ad9/gs9x2hfh9l1vweuk0l151bimhxuvdzxk1p0uvc9i3oalnw82eu7h20i320l0z6if.png)

This categorization helps in organizing and managing access profiles based on vendor-specific settings and configurations. The supported vendor profiles may have pre-configured attributes and templates tailored to the requirements of those specific devices (Ex: Aruba-User-Role, Cisco-AVPair). Devices that do not match any of the supported vendors will still have a default profile assigned to them, allowing for basic access control and management.

A sample role that will assign a specific VLAN is provided below. This example with work for VLAN assignment on most Vendors. For more details on the types of information that should be included in each profile, please consult your vendor’s documentation, or the NAC RADIUS-based Enforcement setup document for your specific vendor.

![](https://uploads.developerhub.io/prod/6Ad9/bb8umyek6tnxu7m8oxwcuc71zvcmsor1e8y11s4xsybduq78y8h3ljgmap38rdoa.png)

If you can not find your desire Vendor listed here, please refer to [this guide](https://www.opswat.com/docs/manac/nac-cloud/vendors) to create your own Vendor

## Managing Access Profiles

1. Log into the **My OPSWAT Central Management** console as an administrator
2. Navigate to  **RADIUS NAC**
3. Click on **Access Profiles** tab
4. On Access Profiles details:
   - To add a new Attribute for a Profile:
     - Click on **Add Attribute Set** button
     - Select an Attribute that match with the supported Vendor
     - Fill in the corresponding Operator & Value
   - To delete an Attribute of a Profile: Click on **Delete** icon
   - To active/ inactive a Profile: Click on the **Toggle** button to switch to a desire status
5. Click on **Save** to apply changes.

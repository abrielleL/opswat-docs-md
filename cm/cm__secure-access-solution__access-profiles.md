<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/access-profiles -->

# Access Profiles

## Overview

An **Access Profile** defines the level of network access a device receives. It is a named set of vendor attributes — a VLAN assignment, a user role, or other access controls — that NAC returns to your network equipment when a device matches a rule.

Access Profiles are the "what access" half of your policy. [Rules](rules) decide *which* devices get a profile; the profile decides *what that access looks like* on the network.

> **Info**
>
> **This page applies to both deployments.** Access Profiles work the same way on [Hybrid NAC](hybrid-nac) and [On-premise NAC](on-premise-nac).

## How Access Profiles Fit Together

1. A device authenticates and is evaluated against your **Rules**.
2. The first matching rule assigns an **Access Profile**.
3. NAC returns that profile's attributes to your switch, controller, or wireless equipment.
4. The equipment applies the access — placing the device on a VLAN, assigning it a role, and so on.

Which attributes are available depends on the [**Vendor**](vendors) you select, because each vendor expects different attributes.

## Before You Start

- Know which VLANs or roles represent each level of access in your network.
- Confirm your network equipment's vendor is available. See [Vendors](vendors) if you need to add a custom one.

## Create an Access Profile

1. Log into the **My OPSWAT Central Management** console as Administrator.
2. Navigate to **RADIUS NAC → Access Profiles**.
3. Click **Add Profile**.
4. Fill in the profile details:

| Field | What to enter |
| ---- | ---- |
| **Name** | A descriptive name for the profile — for example, `Compliance Staff`. |
| **Vendors** | The vendor(s) this profile applies to. This determines which attributes you can set. |

![](https://uploads.developerhub.io/prod/6Ad9/gs9x2hfh9l1vweuk0l151bimhxuvdzxk1p0uvc9i3oalnw82eu7h20i320l0z6if.png)

> **Note**
>
> Devices that do not match any of the supported vendors will still have a default profile assigned to them, allowing for basic access control and management.

## Add Attributes to a Profile

The attributes carry the actual access instruction to your equipment. Vendor profiles include pre-configured attributes and templates tailored to that vendor's requirements.

1. Open the profile and click **Add Attribute Set**.
2. Select an attribute available for the chosen vendor.
3. Complete the operator and value fields.
4. Click **Save**.

![](https://uploads.developerhub.io/prod/6Ad9/bb8umyek6tnxu7m8oxwcuc71zvcmsor1e8y11s4xsybduq78y8h3ljgmap38rdoa.png)

### Common Attributes by Vendor

| Vendor | Attribute | Typical use |
| ---- | ---- | ---- |
| Aruba | `Aruba-User-Role` | Assign a user role, for example a captive-portal redirect role |
| Cisco | `Cisco-AVPair` | Pass vendor-specific access instructions |
| Cisco | `Tunnel-Private-Group-Id` | Assign a VLAN by ID |

<!-- TODO: Extend this table with the other supported vendors and their commonly used attributes. -->

If your vendor is not listed, see [Vendors](vendors) for how to add a custom vendor and enable its vendor-specific attributes.

## Manage Existing Profiles

- **Add Attribute Set** — add further attributes to the profile.
- **Delete** — remove an attribute from the profile.
- **Toggle** — activate or deactivate a profile without deleting it.

Remember to **Save** after making changes.

## Verify the Configuration

1. Connect a test device that should match a rule assigning this profile.
2. In **RADIUS NAC → Sessions**, confirm the device shows the expected **Applied Access Profile**.
3. Confirm on your network equipment that the device landed on the intended VLAN or role.

## Troubleshooting

**The device gets a different profile than expected**

- A different rule matched first. Rule order matters — see [Rules](rules).

**The profile is applied but the device does not get the right access**

- The attributes may not match what your equipment expects. Confirm the attribute and value against your vendor's documentation, and that the correct **Vendor** is selected on the profile.

**The attribute you need is not available**

- It may be a vendor-specific attribute that must be enabled first. See [Vendors](vendors).

## Related Pages

- [Rules](rules) — which devices receive which profile
- [Vendors](vendors) — vendor definitions and vendor-specific attributes
- [Captive Portal Configuration](captive-portal-configuration) — the profile used for captive-portal devices

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)

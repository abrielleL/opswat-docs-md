<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/nac-policy-logic--v8-vs-v10 -->

# Migrating from MD NAC v8 to v10

This guide outlines the available migration paths from MetaDefender NAC v8 to MetaDefender NAC v10. The right approach for your organization depends on your current v8 deployment type. OPSWAT support is available to help you evaluate your options and assist with every step of the migration.

---

## Determine Your Migration Path

Your migration path depends on which network integration type your v8 deployment currently uses:

- **Layer 2 (RADIUS-based) integration** — Proceed to [Path 1: Layer 2 to v10 Migration](https://www.opswat.com/docs/cm/secure-access-solution/nac-policy-logic--v8-vs-v10#path-1-layer-2-to-v10-migration).
- **Layer 3 (Policy Based Routing) integration** — Review [Options for Layer 3 Customers](https://www.opswat.com/docs/cm/secure-access-solution/nac-policy-logic--v8-vs-v10#options-for-layer-3-customers) to choose your approach.

If you are unsure which integration type you are using, OPSWAT support can help you determine this.

---

## Path 1: Layer 2 to v10 Migration

This is the primary migration path for customers whose v8 deployment already uses a Layer 2 RADIUS-based integration.

### **Step 1: Contact OPSWAT Support**

Before beginning, reach out to [OPSWAT Support](https://www.opswat.com/support/contact-support) so we can provision the appropriate software licenses for your deployment.

### **Step 2: Choose a Deployment Model**

MetaDefender NAC v10 supports two deployment models. Choose the one that best fits your infrastructure requirements:

|  | Hybrid / Cloud | Fully On-Premises |
| ---- | ---- | ---- |
| **Management Console** | My OPSWAT Central Management (cloud-hosted) | My OPSWAT Central Management (installed on-prem on Windows or Red Hat 9) |
| **Network Component** | NAC Edge VM, deployed on your local network (preferably on the same VLAN as your existing v8 VM) | NAC Enforcer VM, deployed on your local network |
| **Licensing** | Account flag (provisioned by OPSWAT support) | License key (provided by OPSWAT support) |

### **Step 3: Deploy and Register**

Deploy the NAC Edge or NAC Enforcer VM and register it to your My OPSWAT Central Management instance (cloud or on-prem, respectively).

### **Step 4: Migrate RADIUS Configuration**

OPSWAT support will assist with copying your RADIUS configuration from your v8 environment to v10. Please coordinate with support to schedule this step.

### **Step 5: Set Up a Test Environment**

Before putting v10 into production, set up a test environment to validate functionality:

- Configure a test switch and/or SSID to point at the v10 RADIUS server.
- All network-side settings should remain identical to your v8 configuration — only the RADIUS server IP address need to change.
- Use this test environment to validate your 802.1x, MAB, and/or captive portal workflows against the new system.

### **Step 6: Convert Policies**

NAC v10 uses a simplified policy model compared to v8. The core concepts map as follows:

| NAC v8 | NAC v10 | What Changed |
| ---- | ---- | ---- |
| Qualifier Containers / Sets | Rule Conditions | Conditions now support arbitrary AND/OR nesting rather than the fixed set/container hierarchy. |
| Policy Containers (compliance) | Rule Conditions | Compliance is now just another condition within a Rule, not a separate evaluation layer. |
| Roles | Access Profiles | Functionally identical; renamed to reduce term overloading. |
| Role Matrix | *(removed)* | No longer needed — each Rule maps directly to an Access Profile. |

In v8, determining a device's network access requires three steps: qualify the device into a Policy Group, evaluate compliance against that group's policies, then look up the appropriate Role via the Role Matrix. In v10, this is collapsed into a single step: the system evaluates Rules top-to-bottom, and the first matching Rule directly assigns an Access Profile.

Because of these structural differences, v8 policies cannot be automatically converted to v10 Rules. This conversion must be done manually, and OPSWAT support is happy to assist. This is also a good opportunity to simplify your policy configuration — removing accumulated complexity and refocusing around your current use case.

For a detailed breakdown of the v8 and v10 policy models, see the [NAC Policy Logic: v8 vs. v10](https://www.opswat.com/docs/cm/secure-access-solution/nac-policy-logic--v8-vs--v10) reference document.

### **Step 7: Go Live**

Once testing is complete and policies have been validated, update your production switches and/or SSIDs to point to the v10 RADIUS server.

---

## Options for Layer 3 Customers

Layer 3 (Policy Based Routing) integrations are not currently supported in MetaDefender NAC v10. L3 integrations lack the ability to control east-west traffic, making them less secure than Layer 2 integrations. While limited L3 support may be introduced in a future release, customers currently using L3 have two recommended paths forward:

### **Option A: Migrate v8 from Layer 3 to Layer 2, Then Migrate to v10**

Migrate your existing v8 deployment from a Layer 3 to a Layer 2 integration first, then follow [Path 1: Layer 2 to v10 Migration](https://www.opswat.com/docs/cm/secure-access-solution/nac-policy-logic--v8-vs-v10#path-1-layer-2-to-v10-migration) above.

**This may be a good fit if:**

- You have already begun migrating from L3 to L2 on v8.
- Your existing v8 policies are already close to what you will need on v10.

### **Option B: Implement v10 as a New Deployment**

Start fresh with v10 as a brand-new NAC deployment, rather than migrating your existing configuration.

**This may be a good fit if:**

- You have not yet begun any L3-to-L2 migration on v8.
- Your NAC use case has changed significantly since your v8 policies were originally configured.

---

## Need Help?

OPSWAT is here to help you evaluate the best approach for your organization and to work with you through live sessions to accomplish the migration. Please reach out to [opswat-support@opswat.com](mailto:opswat-support@opswat.com) whenever you are ready to get started.

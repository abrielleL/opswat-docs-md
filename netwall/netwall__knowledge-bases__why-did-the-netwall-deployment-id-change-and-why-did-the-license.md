<!-- source: https://www.opswat.com/docs/netwall/knowledge-bases/why-did-the-netwall-deployment-id-change-and-why-did-the-license -->

# Why did the Netwall Deployment ID change and why did the license become inactive?

**Check Your Version:**

This article applies to all Netwall product versions, including MetaDefender Optical Diode, Unidirectional Security Gateway (USG), Bilateral Security Gateway (BSG), and FEND appliances, etc.

### **Summary**

The Netwall license is bound to the appliance's Deployment ID. If the Deployment ID changes, the license no longer matches and becomes inactive. The message "Deployment IDs do not match" may appear.

### **Symptoms**

- The license becomes inactive.
- The message "Deployment IDs do not match" may appear.

### **Why does the Deployment ID change?**

The Deployment ID is derived from the appliance's hardware and management-network identity. It can regenerate when that identity changes, for example:

1. Replacing or changing the network card (NIC) — a different MAC address will regenerate the Deployment ID.
2. A change to the management interface or management IP/subnet.
3. Other hardware or appliance-level changes.
4. Appliance re-imaging, replacement, or restoration.

### **How to restore a valid license**

If the old Deployment ID is known: contact OPSWAT Support with the old and new Deployment IDs. Support deactivates the old ID, after which the same license can be reactivated against the current Deployment ID via the My OPSWAT portal.

If the old Deployment ID is unknown: either revert the change (the original Deployment ID will reappear), or provide the BLUE-side support package to OPSWAT Support so the previous Deployment ID can be recovered from it and deactivated.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

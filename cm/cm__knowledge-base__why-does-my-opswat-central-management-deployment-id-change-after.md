<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-does-my-opswat-central-management-deployment-id-change-after -->

# Why does my OPSWAT Central Management deployment ID change after a reboot and invalidate my license?

> > > **Check Your Version:** This article applies to My OPSWAT Central Management 10.x on-premises deployments. Automatic license reactivation is planned for the 10.7.26080+ on-premises release.

## **Issue**

After a reboot, power outage, or host failover, My OPSWAT Central Management deployment ID changes. The license activated against the previous deployment ID no longer validates, the license status changes to invalid, license usage resets to `0`, managed endpoints display a warning state, and you must manually reactivate the license.

The deployment ID is used only for licensing and activation. It does not control how OPSWAT Security Agent endpoints reach the server, so a deployment ID change on its own does not disconnect agents. If endpoints also lose connectivity after the same reboot, treat that as a separate symptom.

## **Possible Causes**

The deployment ID is derived from many factors on the server, but the server's **MAC address** and **hostname **are usually the common causes. A change in the deployment ID might mean one of those two inputs changed.

- **Dynamic MAC address on a virtualized host (most common).** Hyper-V virtual machines are assigned dynamic MAC addresses by default. A dynamic MAC can be reassigned when the virtual machine starts on a different cluster node, which happens transparently during live migration or failover — an event you may experience simply as "a reboot." Addressing can appear fully static from inside the guest operating system while the MAC address is still dynamic at the hypervisor level.
- **Hostname change.** Renaming the server, or a rename applied by automation or domain join, also changes the deployment ID. This is rare and is recorded in the Windows System event log.

## **Resolution**

### **1. Confirm whether the MAC address is dynamic**

On the virtualization host, run:

```powershell
Get-VMNetworkAdapter -VMName <VM name> | Select MacAddress, DynamicMacAddressEnabled
```

If `DynamicMacAddressEnabled` returns `True`, the MAC address is not static and is the likely cause. Record the current `MacAddress` value — you will need it in step 3.

### **2. Collect supporting evidence (optional but recommended)**

- Inside the guest, open **Device Manager → View → Show hidden devices → Network adapters**. Ghost or duplicate network adapters are direct evidence that the MAC address changed: Windows enumerates a new adapter each time.
- On the hosts, review the Hyper-V-VMMS event log and Failover Cluster events (for example, event IDs `1201` and `1069`) around the time of each reboot, to correlate the license invalidation with a migration or failover.
- Check the Windows System event log for computer rename events, to rule out a hostname change.

### **3. Set the MAC address to static**

In the virtual machine settings, go to **Network Adapter → Advanced Features → MAC address** and select **Static**.

Assign the **current** MAC address value recorded in step 1. Assigning a different value would itself change the deployment ID and invalidate the license again.

The virtual machine must be powered off to change this setting, so plan a short maintenance window.

### **4. Reactivate the license**

Reactivate the license in My OPSWAT Central Management and confirm that license usage and endpoint status return to normal.

### **5. Validate the fix**

If the virtual machine runs on a cluster, perform one live migration to another node, then re-run the command from step 1 and confirm the MAC address is unchanged. This validates the fix immediately, without waiting for a natural failover.

### **Confirming the cause from My OPSWAT Central Management**

On version 10.6.2605 and later, the support package records that the deployment ID changed and when, which you can correlate with host and Windows event logs to identify which input changed. The change is detected by a scheduled job rather than in real time, so it appears in the logs only after the next scheduler run — up to approximately one day after the triggering reboot. Collect the support package at least a day after a reproduction.

## **Recommendation**

- Set a static MAC address on any virtual machine hosting My OPSWAT Central Management before activating the license.
- Assign the server a static IP address, a DHCP reservation, or preferably a DNS name, and configure endpoints to use the DNS name. This prevents a separate class of endpoint connectivity loss after reboots.
- Upgrade to 10.6.2605 or later so that deployment ID changes are recorded, making any recurrence diagnosable from the support package rather than inferred from symptoms.

> > > **Support:** If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)

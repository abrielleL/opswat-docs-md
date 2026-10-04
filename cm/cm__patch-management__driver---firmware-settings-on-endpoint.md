<!-- source: https://www.opswat.com/docs/cm/patch-management/driver---firmware-settings-on-endpoint -->

# Driver & Firmware Updates

Driver & Firmware Updates extend Patch Management to device drivers, BIOS, and firmware. It continuously detects out‑of‑date drivers and firmware across your fleet, prioritizes them by vendor severity, and lets you approve and deploy them through the same deployment, report, and notification workflows you already use for OS and application patches.

## Driver & Firmware Workflows

Driver & Firmware workflow is integrated directly into existing Patch Management features. Refer to the corresponding guides below for detailed instructions:

| Feature/Area | Guideline |
| ---- | ---- |
| Driver & Firmware Dashboard | [Patch Dashboard](https://www.opswat.com/docs/cm/patch-management/patch-dashboard): Track high-level driver and firmware posture across your fleet. |
| Driver & Firmware Missing Patches List | [Manage Missing Patches: ](https://www.opswat.com/docs/cm/patch-management/manage-missing-patches)View detected driver and BIOS/firmware updates by device or component. |
| Driver & Firmware Job Detail | [Monitor Deployment: ](https://www.opswat.com/docs/cm/patch-management/monitor-deployment)View job progress, ring phases, and device-level result |
| Driver & Firmware Job Deployment | Deploy driver and firmware updates using your preferred method: - [On-Demand Deployment ](https://www.opswat.com/docs/cm/patch-management/on-demand-deployment)for immediate, targeted rollouts - [Policy Deployment ](https://www.opswat.com/docs/cm/patch-management/policy-deployment)for automated, recurring patch schedules - [Ring Deployment ](https://www.opswat.com/docs/cm/patch-management/create-ring-deployment)for phased, staged rollouts across device rings |
| Reports & Notifications | Refer to [Patch Reports & Notifications to ](https://www.opswat.com/docs/cm/patch-management/patch-reports---notification)set up automated email notifications and export compliance reports |
| Air-gapped Patching | Refer to [Air-Gapped Patching - New Patch Management ](https://www.opswat.com/docs/cm/patch-management/air-gapped-patching---new-patch-management)for detailed instruction |

## Driver & Firmware Settings on Endpoint

Administrators can manage how **MetaDefender Endpoint **handles driver and firmware updates on managed devices. This guide covers how to:

- Control the visibility of the **Driver/Firmware Updates** page on the client UI for end-users
- Configure the scan and compliance reporting **interval** for driver and firmware updates

### **Show the Driver/Firmware Updates page on MetaDefender Endpoint**

Control whether the end‑user MetaDefender Endpoint client shows the **Driver/Firmware Updates** page.

![](https://uploads.developerhub.io/prod/97qW/ymfrchoqz2nc4g5ldep5gvj12vic4hnz0pyt19hap78lpo37ii06wd2pg4pgr9sb.png)

1. Navigate to the agent settings:
   1. **Global Level**: Go to Settings > Global > Endpoint Clients > Clients
   2. **Group Level**: Go to Inventory > Groups > [Select Endpoint Group] > Open Settings tab > Go to Agent section
2. Select **Make MetaDefender Endpoint user interface available to end‑users > **Enable **Driver/Firmware Updates**
3. Save

### **Configure the Driver & Firmware interval**

The Driver & Firmware **interval** controls how often endpoints scan for driver & firmware updates, and the freshness window used for compliant reporting.

![](https://uploads.developerhub.io/prod/97qW/a9syptje84vk81sh6hbak73d3c0cpvvgn4gomwvnlkt0ynch7jd9nf2hhsgavfm6.png)

1. Navigate to the compliance report settings:
   - **Global Level:** Go to Settings > Global > Endpoint Clients > Compliance Report section
   - **Group Level:** Go to Inventory > Groups > [Select Endpoint Group] > Settings > Compliance Report section.
2. Set the desired scan and reporting interval. For existing accounts and groups, the interval defaults to the current **OS patch interval** until you change it.
3. Click Save.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)

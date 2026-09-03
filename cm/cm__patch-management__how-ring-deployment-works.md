<!-- source: https://www.opswat.com/docs/cm/patch-management/how-ring-deployment-works -->

# How Ring Deployment Works

A ring deployment is a reusable **configuration** (comparable to a policy) that spawns **runs** each time its schedule fires. Each run processes rings sequentially:

1. **Ring 1 starts**: patch commands are sent to devices in Ring 1.
2. **Progress is tracked**: as devices report results, the success rate for each patch is calculated.
3. **Threshold evaluation**: when installed patches reach the configured success threshold:
   - If **Auto Promote** is enabled, the ring automatically advances to Ring 2.
   - If **Auto Promote** is disabled, the run pauses at **Pending Promote** until a user manually approves progression.
   - If Manual Promote is enabled,
4. **Next ring starts**: the process repeats for Ring 2, Ring 3, and so on.
5. **Completion:**  when the final ring finishes, the run is marked completed and an email report is sent.

See [Create Ring Deployment](https://www.opswat.com/docs/cm/patch-management/create-ring-deployment) for configuration instructions.

### **What is Auto Promote and Manual Promote?**

- **Auto Promote** is a promotion mode in which patches are automatically advanced to the next ring once the success threshold for that ring is met, without requiring any manual intervention.
- **Manual Promote** is a promotion mode in which patches pause at "Pending Promote" after meeting the success threshold, requiring an administrator to review and approve the promotion before the patch advances to the next ring.

### **Independent Patch Promotion**

Each patch is evaluated against the success threshold independently and move to next ring individually. This means different patches in the same deployment can be at different rings at the same time, each moving at its own pace.

### R**ing Schedule **

| Recurrence | Use it when |
| ---- | ---- |
| Daily | You want the deployment to run every day |
| Weekly | You want a predictable cadence on specific days of the week |
| Monthly | You want a predictable cadence on specific days of the month |
| Monthly, Patch Tuesday | You want your OS patch cadence to follow Microsoft's monthly release, offset by a set number of days |
| One Time | You want a single, controlled rollout at a specific date and time |
| One Time, Manual Start | You want a single rollout that only begins when you click **Start** |

### **Maintenance Window**

Even after a patch is promoted to a ring, it does not install on devices immediately. The Maintenance Window tells the MetaDefender Endpoint agent on each endpoint **the permitted time window to perform patch installation**. Patches wait in a queue on the device and are only installed when the next maintenance window opens.

This protects end-users from unexpected interruptions, for example, you can restrict patching to nights and weekends so that devices used during business hours are never disrupted mid-work.

> **Info**
>
> If no patches are ready, that window is skipped and the process continues at the next scheduled window.

| Recurrence | Date & Time | Description |
| ---- | ---- | ---- |
| **Daily** | From time, To time, Timezone | Opens a patching window every day between the specified hours. |
| **Weekly** | On Days (Mon–Sun), From time, To time, Timezone | Opens a patching window on the selected days of the week. |
| **Monthly** | On Days (calendar grid), From time, To time, Timezone | Opens a patching window on the selected days of the month. |

### Targets for Ring Deployment

Each ring is a self-contained stage with its own targets, promotion rule, and success threshold. Rings run in order. Ring 1 must complete before Ring 2 begins, and so on. You can configure up to 10 rings, and at least one is required.

Each ring is independently configurable:

- **Naming**: Each ring is created with a default name (Ring 1, Ring 2, etc.). You can rename it to match your rollout strategy (e.g., Canary, Early Adopter, or Production).
- **Target type**: Choose whether to apply the ring to device groups or individual devices. Each ring can use a different targeting method.
- **Promotion**: Determines how patches move to the next ring after results are collected:
  - **Auto**: Patches move to the next ring automatically once the success threshold is met.
  - **Manual**: Admins review results and manually approve promotion.
- **Success Threshold**: The percentage of targeted devices that must successfully install the patch before it moves to the next ring (available when Auto promotion is selected).

## Related Resources

- [Missing Patches: ](https://www.opswat.com/docs/cm/patch-management/manage-missing-patches)Find and act on missing patches and outdated application across your environment
- [Patch Dashboard](https://www.opswat.com/docs/cm/patch-management/patch-dashboard): Get a single-pane view of your environment's patch posture
- [Custom Patch Reports](https://www.opswat.com/docs/cm/patch-management/custom-patch-reports): Configure point-in-time patch reports

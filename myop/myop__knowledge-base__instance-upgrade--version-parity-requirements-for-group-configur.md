<!-- source: https://www.opswat.com/docs/myop/knowledge-base/instance-upgrade--version-parity-requirements-for-group-configur -->

# Kiosk Upgrade: Version Parity Requirements for Group Configuration Management

### [**Overview**](/docs/myop/knowledge-base/instance-upgrade--version-parity-requirements-for-group-configur#overview)

In My **OPSWAT Central Management,** Kiosk instances are typically managed in Groups. This allows administrators to define a "Group Configuration" based on a specific instance and deploy those settings across all other instances within the group.

For this mechanism to function, **version parity** is a strict requirement between the source (template) instance and the target instances.

### [**Known Limitation**](/docs/myop/knowledge-base/instance-upgrade--version-parity-requirements-for-group-configur#known-limitation)

**Symptoms:**

- A **"NOT COMPATIBLE"** warning appears on the My OPSWAT Central Management instance list.
- The "Apply Configuration" action is disabled or fails for instances running a different version.

[Note This limitation is resolved in My OPSWAT Central Management 10 version with Kiosk 4.7.11](/docs/myop)

**Typical Scenario:**

1. A group of 10 Kiosks is running v4.5.0 using a shared Group Configuration.
2. An administrator upgrades 2 instances to v4.6.0 to test new security features.
3. These 2 upgraded instances now deviate from the Group Configuration (which remains anchored to v4.5.0).
4. Any subsequent updates made at the Group level **will fail to apply** to the 2 upgraded instances until the entire group is uniform.

### [Recommended Kiosk Upgrade Procedure](/docs/myop/knowledge-base/instance-upgrade--version-parity-requirements-for-group-configur#recommended-kiosk-upgrade-procedure)

1. **Baseline Synchronization**

Apply the current group configuration to all Kiosk instances to ensure every device has configration synchronized

2. **Managed Upgrade**

Execute the Kiosk software upgrade across the group; expect temporary "Version Mismatch" warnings My OPSWAT Central Management as instances move to the newer version.

3. **Configuration Promotion**

Select one upgraded instance, verify its settings, and set it as the new Group Configuration to re-establish the baseline and then re-apply the configuration to all group instances to restore full compatibility.

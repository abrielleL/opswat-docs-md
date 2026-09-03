<!-- source: https://www.opswat.com/docs/manac/knowledge-base/how-to-toggle-enforcement-on-layer-2-or-layer-3-networks--rbe-pb -->

# How To Toggle Enforcement on Layer 2 or Layer 3 networks (RBE/PBR)?

This article applies to a range of supported network management devices, the current NAC Enforcer and the Web UI.

When **Enforcement** is enabled, all devices under the configured **Enforcement Device** will be placed under the associated **Policy**.

To toggle enforcement on your network, follow the network-appropriate steps below.

## [Layer 2 / Radius Based Enforcement / RBE](/docs/manac/knowledge-base/how-to-toggle-enforcement-on-layer-2-or-layer-3-networks--rbe-pb#layer-2--radius-based-enforcement--rbe)

1. Navigate to **RADIUS>Configuration.** Select **Authentication and Enforcement

** 2. Select **Mode** and **Authentication Type

** 3. Define a **Vendor

** 4. Specify a **NAS** corresponding with the previous selected **Vendor

** 5. **Apply and Use** the current configuration

6. Then, back to the **Server** tab and click on Enable**

** 7. Click on OK

Pro Tip:

To confirm that enforcement is enabled, look at the Status icon, which will now appear green (or red when enforcement has is disabled).

## [Layer 3 / Policy Based Routing / PBR](/docs/manac/knowledge-base/how-to-toggle-enforcement-on-layer-2-or-layer-3-networks--rbe-pb#layer-3--policy-based-routing--pbr)

1. Go to your **NAC Dashboard>Configuration>Enforcement Setup>Routers/Switches**.
2. Then click **Enable** alongside your chosen L3 routing device connection, or, in the top right-hand corner of the screen, click **Enable All**.

3. The router should now show a **Green** checkmark, indicating its enabled status.

## [Disabling Enforcement](/docs/manac/knowledge-base/how-to-toggle-enforcement-on-layer-2-or-layer-3-networks--rbe-pb#disabling-enforcement)

Please Note:

Disabling enforcement will place your network in a **fail-open** state, opening your network to possible attack in the event of a failure.

Please follow the network-specific steps below to disable enforcement.

### [Disabling Layer 2 / Radius Based Enforcement / RBE](/docs/manac/knowledge-base/how-to-toggle-enforcement-on-layer-2-or-layer-3-networks--rbe-pb#disabling-layer-2--radius-based-enforcement--rbe)

1. Go to your **NAC Dashboard>Configuration>Radius>Configuration**.
2. Then, alongside the **Status** icon, click **Disable**, as shown below, then click **OK** in the pop-up box to confirm.

3. The enforcement **Status** icon will now appear in red, indicating that enforcement is disabled.

### [Disabling Layer 3 / Policy Based Routing / PBR](/docs/manac/knowledge-base/how-to-toggle-enforcement-on-layer-2-or-layer-3-networks--rbe-pb#disabling-layer-3--policy-based-routing--pbr)

1. Go to your **NAC Dashboard>Configuration>Enforcement Setup>Routers/Switches**.
2. Then click **Disable** alongside your chosen L3 routing device connection, or, in the top right-hand corner of the screen, click **Disable All**.

3. In the pop-up, add an optional note for change management, then click **Submit**.

4. The router should now display a **Red** checkmark, indicating its disabled status.

Support:

If you have followed the instructions above but have been unable to **Toggle Enforcement On Layer 2 / Layer 3 (RBE/PBR) Networks**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

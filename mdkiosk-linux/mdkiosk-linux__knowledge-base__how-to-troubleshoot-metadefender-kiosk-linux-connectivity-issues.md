<!-- source: https://www.opswat.com/docs/mdkiosk-linux/knowledge-base/how-to-troubleshoot-metadefender-kiosk-linux-connectivity-issues -->

# How to Troubleshoot MetaDefender Kiosk Linux Connectivity Issues and “Incompatible MyOPSWAT Instance” Error (Including Re-Imaging as Last Resort)?

**Check Your Version:**

This article applies to MetaDefender Kiosk Linux v5.x.x instances that are managed by OPSWAT Central Management v7.

## [**Overview**](/docs/mdkiosk-linux/knowledge-base/how-to-troubleshoot-metadefender-kiosk-linux-connectivity-issues#overview)

This article describes how to troubleshoot MetaDefender Kiosk Linux when it shows the error:

**Incompatible MyOPSWAT instance - The transfer USB you have inserted is not registered with the connected MyOPSWAT. Please use a Kiosk onboarded to the correct MyOPSWAT.**

- The Kiosk is expected to be managed by Central Management on-prem (OCM), not directly by a MyOPSWAT cloud tenant.
- The device appears unusable because this message is shown whenever a transfer USB is inserted.

In this situation, the Kiosk is typically still bound to a different or stale management context (old MyOPSWAT instance or incorrect management configuration). The recommended approach is:

- Collect the correct management details from OCM.
- Perform a System Reset to clear the existing configuration.
- Re-onboard the Kiosk to the correct Central Management server.

**A full re-image of the Kiosk appliance is only needed if the unit cannot be recovered with the steps provided above.**

## [**When to Use This Article (Typical Symptoms)**](/docs/mdkiosk-linux/knowledge-base/how-to-troubleshoot-metadefender-kiosk-linux-connectivity-issues#when-to-use-this-article-typical-symptoms)

- You see the “Incompatible MyOPSWAT instance” message when inserting a transfer USB into MetaDefender Kiosk Linux.
- The environment is using OPSWAT Central Management on-prem as the management server for Kiosk Linux.
- In OCM you can see a Kiosk Linux instance but cannot easily see its exact IP address.
- The Kiosk is otherwise booting and showing its UI, but the error effectively makes it unusable.

## [**Necessary Steps**](/docs/mdkiosk-linux/knowledge-base/how-to-troubleshoot-metadefender-kiosk-linux-connectivity-issues#necessary-steps)

### [**1. Collect the Correct Management Details from Central Management**](/docs/mdkiosk-linux/knowledge-base/how-to-troubleshoot-metadefender-kiosk-linux-connectivity-issues#1-collect-the-correct-management-details-from-central-management)

Before touching the Kiosk, collect the two key values required to onboard (or re-onboard) the Kiosk to Central Management:

1. Log in to the OCM console.
2. Go to Settings → Server Configuration → Server URL.

- This is the Hostname / Server URL that Kiosk must use for the management connection.
- OCM documentation describes this as the Server URL used by managed products to reach the server.

3. Go to Settings → Global Settings → ACCOUNT → Registration Code.

- This Registration Code is the integration secret Kiosk uses to enroll into Central Management.

Keep these two values handy; you will enter them on the Kiosk during onboarding.

[Adding a MetaDefender Kiosk Linux instance - OPSWAT Central Management v7 - Legacy](https://www.opswat.com/docs/ocm/integrations/adding-a-metadefender-kiosk-linux-instance)

### [**2. Reset the Kiosk (System Reset) to Clear Old Management Bindings**](/docs/mdkiosk-linux/knowledge-base/how-to-troubleshoot-metadefender-kiosk-linux-connectivity-issues#2-reset-the-kiosk-system-reset-to-clear-old-management-bindings)

If the Kiosk still boots to the UI and shows the splash screen, use a System Reset to wipe its configuration and allow a clean re-onboarding.

What a System Reset does:

- Returns Kiosk to a reconfigurable state.
- Clears configuration, including existing management bindings (MyOPSWAT / Central Management).
- Removes queued reports that have not yet been sent to Central Management.

**High-level System Reset procedure (Linux Kiosk):**

1. Hold down the power button to shut down the system.
2. Connect a keyboard to the Kiosk.
3. Power the Kiosk back on.
4. When the OPSWAT MetaDefender Kiosk splash screen text appears, hold down the documented keys (for example, LEFT-SHIFT + LEFT-ALT + F7 or LEFT-SHIFT + LEFT-ALT + F9 depending on version).

5. Continue to hold the keys until the system reboots.
6. On success, a language selection or initial setup screen appears, indicating that Kiosk is reset and ready to be configured again.

At this point, the previous MyOPSWAT / OCM association is cleared, which is essential for resolving stale “Incompatible MyOPSWAT instance” behavior.

- If you cannot trigger System Reset (for example, the unit never reaches the splash screen or is stuck in a hard boot loop), skip ahead to Section 5 – Re-Imaging as a Last Resort.

<https://www.opswat.com/docs/mdkiosk-linux/v5.7.4/troubleshooting/troubleshooting#system-reset>

### [**3. Onboard the Kiosk Back to Central Management (Ethernet / Wi-Fi Mode)**](/docs/mdkiosk-linux/knowledge-base/how-to-troubleshoot-metadefender-kiosk-linux-connectivity-issues#3-onboard-the-kiosk-back-to-central-management-ethernet--wi-fi-mode)

After a successful System Reset, you must re-onboard the Kiosk to the correct management server using Ethernet / Wi-Fi Mode.

**3.1. Configure Network Connectivity**

On the Kiosk UI:

1. Open the network / management configuration screen.
2. Ensure the Kiosk has a valid IP address:

- If networking is working, Kiosk automatically detects and shows its IP.
- If the field is empty, use the gear icon or network settings to configure Ethernet or Wi-Fi.

[Management - Ethernet / Wi-Fi Mode - MetaDefender Kiosk Linux](https://www.opswat.com/docs/mdkiosk-linux/setup/management-via-ethernet---wi-fi-mode)

**3.2. Connect to Central Management**

When prompted to connect to a management server (OCM or MyOPSWAT):

1. Select Ethernet / Wi-Fi Mode as the operation / management mode.
2. Enter the values collected from OCM:

- Hostname / Server URL:

Paste the Server URL from OCM (Settings → Server Configuration → Server URL).

- Registration Code:

Paste the Registration Code from OCM (Settings → Global Settings → ACCOUNT → Registration Code).

- Optionally set a recognizable Kiosk Name.

3. Confirm / click Connect. If the connection succeeds, Kiosk completes its onboarding and registers as a managed instance.

**3.3. Note for OCM-Only Environments**

If the environment uses Central Management on-prem only (no active MyOPSWAT media registration or Island Mode workflow):

- Only configure OCM’s Server URL and Registration Code.
- Do not re-associate the Kiosk with an old MyOPSWAT instance or an old Island Mode transfer USB.
- Once onboarded to the correct OCM server, the “Incompatible MyOPSWAT instance” error related to previously registered media should no longer appear.

### [**4. Verify That the Kiosk Is Managed Again and Retrieve System Details**](/docs/mdkiosk-linux/knowledge-base/how-to-troubleshoot-metadefender-kiosk-linux-connectivity-issues#4-verify-that-the-kiosk-is-managed-again-and-retrieve-system-details)

**4.1. Verify Connectivity in Central Management**

In OCM:

1. Go to Inventory → MetaDefender Kiosk Linux → Instances.
2. Confirm that:

- The Kiosk appears in the list as a MetaDefender Kiosk Linux instance.
- It shows a Connected or healthy status and version details.

This confirms the Kiosk is under management again and should be operating with the correct configuration.

**4.2. Seeing the Kiosk IP Address and System Settings**

In some OCM builds, the Linux Kiosk IP is not displayed directly in the instance list. To obtain detailed system info, including IP:

1. Enable or use the exit password for the Kiosk UI, if configured. The “Enable Exit Password for Kiosk UI” and related Kiosk hardening documentation describe how to protect Kiosk UI exit and how exit passwords work.

<https://www.opswat.com/docs/mdkiosk/v4.7.8/hardened-image/enable-exit-password-for-kiosk-ui>

2. Exit the Kiosk UI to reach the underlying Linux OS.
3. From the Linux shell, use standard tools (for example, `ip addr`) or your DHCP/server logs to determine the Kiosk IP address and other network parameters.

This is the practical workaround when OCM does not show the IP address explicitly but you need to verify network and connectivity details.

### [**5. Re-Imaging the Linux Kiosk (Last Resort Only)**](/docs/mdkiosk-linux/knowledge-base/how-to-troubleshoot-metadefender-kiosk-linux-connectivity-issues#5-re-imaging-the-linux-kiosk-last-resort-only)

Re-imaging is not the normal fix for connectivity or “Incompatible MyOPSWAT instance” problems if the Kiosk is able to:

- Boot to the splash screen, and
- Successfully perform a System Reset to allow reconfiguration.

**Only consider re-imaging when all of the following are true:**

- **The Kiosk is stuck in a persistent boot loop or fails to reach the UI.**
- **System Reset cannot be successfully triggered (the key sequence never works, or the device fails before the splash screen).**
- **The unit cannot be brought back to a usable, re-onboardable state through normal troubleshooting.**

OPSWAT documentation for hardened Kiosk images explicitly notes re-imaging as the necessary step in certain unrecoverable cases (for example, when the exit password cannot be recovered and no remote management method works).

OPSWAT

**5.1. Before Requesting a Re-Image**

If the Kiosk is still able to reach its UI at any point in the boot sequence, generate a support package and provide it to OPSWAT Support. The Kiosk Linux troubleshooting documentation explains how to create a support package, which contains logs and system information used for analysis.

**5.2. Requesting an Official Re-Imaging Image and Procedure**

1. Open a case with OPSWAT Support via the OPSWAT Support portal.
2. Provide:

- Product versions (MetaDefender Kiosk Linux, OCM).
- Clear description of the issue (boot loop, System Reset failing, etc.).
- Steps already attempted (System Reset, re-onboarding, network checks).
- The support package if one was successfully created.

3. OPSWAT Support will:

- Provide the correct, hardware-compatible Kiosk image.
- Provide the step-by-step re-imaging procedure (typically USB media + BIOS/boot configuration).

4. After re-imaging, repeat the steps in Sections 3–6 to connect the Kiosk to Central Management again.

Re-imaging will completely wipe the appliance (configuration, local logs, and queued reports), so it should remain the last resort after System Reset and re-onboarding options have been exhausted.

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).

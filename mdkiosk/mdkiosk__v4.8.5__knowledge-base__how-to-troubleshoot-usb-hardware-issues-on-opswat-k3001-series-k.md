<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-to-troubleshoot-usb-hardware-issues-on-opswat-k3001-series-k -->

# How to Troubleshoot USB Hardware Issues on OPSWAT K3001 Series KIOSK?

**Check Your Version:** This article applies to MetaDefender Kiosk and is applicable for all OPSWAT K3001 Series KIOSK USB hardware-related troubleshooting. It covers deployments on Hardened Image (Windows-based), both Internet-connected or Air-gapped, and on-premise installations.

## [**Issue**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-troubleshoot-usb-hardware-issues-on-opswat-k3001-series-k#issue)

USB hardware-related issues on the OPSWAT K3001 Series KIOSK, including:

- USB ports not detecting devices
- USB ports physically broken or displaced
- Intermittent USB connectivity
- No power to USB ports
- Peripheral devices not recognized despite correct drivers

## [**Hardware Troubleshooting Workflow**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-troubleshoot-usb-hardware-issues-on-opswat-k3001-series-k#hardware-troubleshooting-workflow)

Always follow the steps below **in order** to correctly isolate the issue.

---

### [**Step 1: Visual & Physical Inspection**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-troubleshoot-usb-hardware-issues-on-opswat-k3001-series-k#step-1-visual--physical-inspection)

1. Inspect all front-facing USB ports:

   - Top panel USB ports (USB-A / USB-C)
   - USB port below the MicroSD slot
2. Check for:

   - Bent pins
   - Loose or sunken ports
   - Physical displacement from chassis
3. Confirm whether the issue affects:

   - A single port
   - Multiple ports
   - All USB ports

> If physical damage is visible, continue to **Step 4** directly.

---

### [**Step 2: BIOS Verification**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-troubleshoot-usb-hardware-issues-on-opswat-k3001-series-k#step-2-bios-verification)

1. Reboot the KIOSK
2. Press **F12** during startup
3. Enter **BIOS Setup**
4. Navigate to: **Integrated Devices → USB / Thunderbolt Configuration**
5. Ensure the following option is enabled:

   - **Enable External USB Ports**
6. Save changes and reboot

---

### [**Step 3: Operating System & Driver Validation**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-troubleshoot-usb-hardware-issues-on-opswat-k3001-series-k#step-3-operating-system--driver-validation)

1. Log in to Windows on the KIOSK
2. Open **Device Manager**
3. Expand **Universal Serial Bus Controllers**
4. Verify there are no warning icons on USB devices
5. Reinstall USB drivers if required:

   - Right-click each **USB Root Hub** → Uninstall
   - Reboot the system

> Note: Internet access is **not required** for driver reinstallation.

---

### [**Step 4: Internal Hardware Isolation**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-troubleshoot-usb-hardware-issues-on-opswat-k3001-series-k#step-4-internal-hardware-isolation)

> Perform this step only if software and BIOS checks are clean.

**4.1 Inspect Internal USB Cabling**

1. Power off the KIOSK
2. Open the rear access panel
3. Verify internal USB cables are:

   - Firmly seated
   - Not pinched or damaged

**4.2 Trace Cable to StarTech USB Adapter**

1. Follow the internal USB cable to the [**StarTech.com**](http://StarTech.com) **USB adapter**
2. Confirm:

   - Adapter has power
   - Power cable is connected securely
   - If it is correctly plugged in, follow the cable (note down the cable number) and make sure that it is correctly connected to the [StarTech.com](http://StarTech.com) USB adapter as shown in the screenshot given below.

**4.3 Port & Cable Testing**

1. Disconnect the USB cable from the kiosk front panel
2. Connect it directly to a laptop
3. Plug a USB device into the front USB port
4. Validate whether the device is detected

**4.4 Cross-Test with Secondary Adapter (if available)**

- Move the cable to another available StarTech adapter port
- Re-test USB functionality

---

**Step 5: CPU Connectivity Check**

1. Ensure at least one cable from the StarTech adapter is connected to the CPU box under the KIOSK
2. Confirm that the [StarTech.com](http://StarTech.com) adapter power cable is correctly plugged in to the power socket along with other cables.

---

## [**Decision Matrix**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-troubleshoot-usb-hardware-issues-on-opswat-k3001-series-k#decision-matrix)

| Observation | Conclusion |
| --- | --- |
| USB works on laptop but not on kiosk | Front USB port or adapter fault |
| No USB power or detection at all | Adapter or power issue |
| Visible physical damage | Hardware replacement required |
| BIOS / driver issue resolves problem | Software-related |

## [**When to Proceed with Hardware Replacement**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-troubleshoot-usb-hardware-issues-on-opswat-k3001-series-k#when-to-proceed-with-hardware-replacement)

Proceed with hardware replacement request if **any** of the following are true:

- USB ports are physically damaged
- Ports are displaced or broken
- Internal connectors are damaged
- Issue persists after all isolation steps

---

## [**How to Report a Hardware Issue (Required Details)**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-troubleshoot-usb-hardware-issues-on-opswat-k3001-series-k#how-to-report-a-hardware-issue-required-details)

When opening a support case, **all details below are mandatory**:

- Customer Name:
- Partner / Distributor Name (if applicable):
- End Customer Name:
- KIOSK Model: K3001 Series
- Serial Number (SN):
- Issue Description:
- Affected Ports / Components:
- Troubleshooting Steps Performed:
- Photos of Damage (clear images):
- Site Environment (Air-gapped / Internet-connected):
- Contact Name:
- Contact Phone:
- Contact Email:
- Shipping Address:
- Reported By:
- VAT Number (if applicable):

---

## [**Best Practices**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-troubleshoot-usb-hardware-issues-on-opswat-k3001-series-k#best-practices)

- Always attach **clear photos** of the affected hardware
- Confirm whether the site is air-gapped early
- Perform isolation steps before requesting onsite support
- Clearly state if the issue is **physical** vs **functional**

**Support:** If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

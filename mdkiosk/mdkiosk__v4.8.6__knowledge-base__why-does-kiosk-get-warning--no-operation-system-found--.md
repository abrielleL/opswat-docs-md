<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found-- -->

# Why does kiosk get warning "No operation system found"?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

 **Check Your Version:**

This article applies to all MetaDefender Kiosk version

## [**Issue**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found--#issue)

The kiosk displays the following warning during startup: No operating system found

## [**Possible causes**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found--#possible-causes)

This usually means the kiosk is unable to locate or boot from the Windows boot partition.

This issue may be caused by one or more of the following:

- **Incorrect boot sequence** in BIOS.
- **Windows Boot Manager is missing or not listed** in the BIOS boot options.
- **Corrupted boot configuration data**, also known as BCD.
- **Fast Startup or an unexpected shutdown** causing the system to boot from a previous failed state.
- **Missing or damaged boot partition**.
- **Faulty storage drive or other hardware issue**.

## [**Resolutions**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found--#resolutions)

Please try the following steps.

### [**1. Power Cycle the Kiosk**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found--#1-power-cycle-the-kiosk)

1. Power off the kiosk.
2. Unplug the power cable.
3. Wait for a few minutes.
4. Reconnect the power cable.
5. Power on the kiosk and check whether the issue is resolved.

### [**2. Check the BIOS Boot Sequence**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found--#2-check-the-bios-boot-sequence)

1. Restart the kiosk.
2. Enter the BIOS setup menu. This is usually done by pressing **Del**, **F2**, **F12**, or **Esc** during startup, depending on the kiosk model.
3. Locate the **Boot Sequence** or **Boot Order** settings.
4. Confirm that **Windows Boot Manager** is listed.
5. Make sure **Windows Boot Manager** is at the top of the primary boot sequence.
6. Save the BIOS changes and reboot the kiosk.

### [**3. If Windows Boot Manager Is Listed**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found--#3-if-windows-boot-manager-is-listed)

If **Windows Boot Manager** is listed but is not the first boot option:

1. Move **Windows Boot Manager** to the top of the boot sequence.
2. Save the BIOS settings.
3. Reboot the kiosk.
4. Confirm whether the kiosk can boot successfully.

### [**4. If Windows Boot Manager Is Missing**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found--#4-if-windows-boot-manager-is-missing)

If **Windows Boot Manager** is not listed in BIOS, the Windows boot configuration may be corrupted.

This can happen after an unexpected shutdown, power interruption, failed reboot, or other system-level issue.

Please confirm whether the kiosk experienced any unexpected shutdowns, forced reboots, or power loss before the issue occurred.

For Lenovo kiosks, there may be multiple boot sequence options. Please verify that **Windows Boot Manager** is present in all applicable boot sequence sections.

### [**5. Disable Fast Startup**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found--#5-disable-fast-startup)

Fast Startup may sometimes cause the system to resume from a previous failed boot state.

If the kiosk can still boot into Windows intermittently, disable Fast Startup:

1. Open **Control Panel**.
2. Go to **Power Options**.
3. Select **Choose what the power buttons do**.
4. Click **Change settings that are currently unavailable**.
5. Uncheck **Turn on fast startup**.
6. Save the changes.
7. Restart the kiosk.

### [**6. Reimage the Kiosk**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found--#6-reimage-the-kiosk)

If the boot configuration is corrupted and the kiosk cannot boot into Windows, reimaging the kiosk may be required.

Please follow the standard kiosk reimaging procedure for your environment.

### [**7. Check for Hardware Issues**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found--#7-check-for-hardware-issues)

If the issue persists after checking the BIOS boot order and reimaging the kiosk, the storage drive or another hardware component may be faulty.

In this case, OPSWAT Support may need to proceed with hardware replacement or RMA after further verification.

## [**Information to Provide to OPSWAT Support**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-kiosk-get-warning--no-operation-system-found--#information-to-provide-to-opswat-support)

To help us investigate further, please provide the following information:

- A photo of the error message.
- Photos of the BIOS boot sequence screens.
- Confirmation whether **Windows Boot Manager** is listed in BIOS.
- Confirmation whether the kiosk had any unexpected shutdown, power loss, or forced reboot before the issue started.
- Kiosk serial number.
- Whether reimaging was attempted and the result.

**Support:** If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

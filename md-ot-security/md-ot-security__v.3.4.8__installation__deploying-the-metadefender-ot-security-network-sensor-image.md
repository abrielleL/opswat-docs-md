<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-network-sensor-image -->

# Deploying the MetaDefender OT Security Network Sensor image file

## [About this task](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-network-sensor-image#about-this-task)

Use this procedure to deploy the MetaDefender OT Security Network Sensor image file on an Industrial PC (DIN-rail) or 1U Short Depth

## [Before you begin](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-network-sensor-image#before-you-begin)

- Obtain the latest Network Sensor Linux image file from <https://my.opswat.com/home/metaDefender-ot-security>

## [Procedure](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-network-sensor-image#procedure)

### [1. Create MetaDefender OT Security USB](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-network-sensor-image#1-create-metadefender-ot-security-usb)

The installation of MetaDefender OT Security requires using a USB boot created from a downloadable image file:

1.1. Download the MetaDefender OT Security zip file that stores the **MDOTS_Network SensorManagement_x.x.x.img** disk image. You must extract the zip file using an extracting tool from Windows.

1.2. Download the **Rufus** tool for USB burning.

1.3. Plug in a flash USB with **at least 32GB** of storage.

1.4. Format the USB using the **exFAT file system** type with Windows' format tool. Only use quick format if the USB file system is already exFAT.

1.5. Open Rufus, select the USB device, and choose the MetaDefender OT Security image file. The select file system is Large FAT32.

1.6. Start to burn the USB.

1.7. Wait for the process to finish.

1.8. Plug out the USB.

### [2. BIOS Configuration](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-network-sensor-image#2-bios-configuration)

### [2.1. Industrial PC (DIN-rail) - Reorder Boot Sequence](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-network-sensor-image#21-industrial-pc-din-rail---reorder-boot-sequence)

This section supports **reordering the boot sequence and prioritizing the USB boot first** if the installing machine is an industrial PC.

Before installation, the user needs to configure the **BIOS setting** of that industrial PC for the MetaDefender OT Security USB boot setup.

1. Start the machine.
2. After starting for a few seconds, press the **Delete button** to enter the BIOS menu interface.
3. Navigate to the **Boot** option
4. Change to Boot Option **#1** to **[USB Device]**

The default setting of the Boot setup

### [3. MetaDefender OT Security Network Sensor flashing and installation](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-network-sensor-image#3-metadefender-ot-security-network-sensor-flashing-and-installation)

In the last section, the only thing left is to install MetaDefender OT Security onto the machine, which is accomplished almost automatically by the system.

3.1. Plug in the **MetaDefender OT Security USB** that the user created in the first step.

3.2. Boot to the USB from the BIOS. Pay attention to the USB brand name to avoid choosing the wrong one.

3.3. Wait for the first stage installation until the popup asking to wipe all data shows up.

3.4. Select **Yes** and wait until the flashing completed popup shows.

3.5. Press **OK** and wait for the machine to **turn off**.

3.6. **Unplug** USB **(Important!!!)**

3.7. **Turn on** the machine again.

From now on, users only need to wait for approximately 10-15 minutes for the final installation. It is essential not to turn off the machine until the installation is complete.

After this, the MetaDefender OT Security Network Sensor will automatically start and enter the management console application

## [Next Steps](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-network-sensor-image#next-steps)

- Configuration for Network Sensor on local management console application.

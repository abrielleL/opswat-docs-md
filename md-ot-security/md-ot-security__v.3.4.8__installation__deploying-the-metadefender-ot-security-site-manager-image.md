<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-site-manager-image -->

# Deploying the MetaDefender OT Security Site Manager image file

## [About this task](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-site-manager-image#about-this-task)

Use this procedure to deploy the MetaDefender OT Security Site Manger image file

## [Before you begin](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-site-manager-image#before-you-begin)

- Obtain the latest Site Manager Linux image file from <https://my.opswat.com/home/metaDefender-ot-security>

## [Procedure](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-site-manager-image#procedure)

### [1. Create MetaDefender OT Security USB](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-site-manager-image#1-create-metadefender-ot-security-usb)

The installation of MetaDefender OT Security requires using a USB boot created from a downloadable image file: 1.1. Download the MetaDefender OT Security zip file that stores the **MDOTS_SiteManagement_x.x.x.img** disk image. You must extract the zip file using an extracting tool from Windows.

1.2. Download the **Rufus** tool for USB burning.

1.3. Plug in a flash USB with **at least 32GB** of storage.

1.4. Format the USB using the **exFAT file system** type with Windows' format tool. Only use quick format if the USB file system is already exFAT.

1.5. Open Rufus, select the USB device, and choose the MetaDefender OT Security image file. The select file system is Large FAT32.

1.6. Start to burn the USB.

1.7. Wait for the process to finish.

1.8. Plug out the USB.

### [2. BIOS Configuration](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-site-manager-image#2-bios-configuration)

### [OptiPlex 7400 All-In-One](https://www.dell.com/en-us/shop/desktop-computers/optiplex-7400-all-in-one/spd/optiplex-7400-aio/gctoo7400aiousvp) - Storage configuration

This section is only required if the installing machine is [OptiPlex 7400 All-In-One](https://www.dell.com/en-us/shop/desktop-computers/optiplex-7400-all-in-one/spd/optiplex-7400-aio/gctoo7400aiousvp).

Before installation, the user needs to configure the **BIOS setting** of that All-In-One machine for the MetaDefender OT Security USB boot setup.

2.1. Start the machine.

2.2. After starting for a few seconds, press the **F2 button** to enter the BIOS menu interface.

2.3. At the **BIOS menu**, go to the **Storage** tab, section **SATA/NVMe Operation**.

2.4. Click option **AHCI/NVMe** to enable the storage device to be configured for **AHCI/NVMe** mode.

### [3. MetaDefender OT Security Site Manager flashing and installation](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-site-manager-image#3-metadefender-ot-security-site-manager-flashing-and-installation)

In the last section, the only thing left is to install MetaDefender OT Security onto the machine, which is accomplished almost automatically by the system.

3.1. Plug in the **MetaDefender OT Security USB** that the user created in the first step.

3.2. Boot to the USB from the BIOS. Pay attention to the USB brand name to avoid choosing the wrong one.

3.3. Wait for the first stage installation until the popup asking to wipe all data shows up.

3.4. Select **Yes** and wait until the flashing completed popup shows.

3.5. Press **OK** and wait for the machine to **turn off**.

3.6. **Unplug** USB **(Important!!!)**

3.7. **Turn on** the machine again.

From now on, users only need to wait for approximately 10-15 minutes for the final installation. It is essential not to turn off the machine until the installation is complete.

After this, the MetaDefender OT Security Site Manager will automatically start and enter the management console application

## [Next Steps](/docs/md-ot-security/v.3.4.8/installation/deploying-the-metadefender-ot-security-site-manager-image#next-steps)

- Configuration for Site Manager on local management console application.

<!-- source: https://www.opswat.com/docs/md-ot-security/installation/iso-esxi-installation -->

# Deploying MetaDefender OT Security ISO Using Host Client on ESXi Host

## [About this task](/docs/md-ot-security/installation/iso-esxi-installation#about-this-task)

*Starting from version 4.0.0, MetaDefender OT Security supports installation via* an *ISO file.*

Use this procedure to deploy MetaDefender OT Security ISO on vCenter using the Host Client.

## [Before you begin](/docs/md-ot-security/installation/iso-esxi-installation#before-you-begin)

Note

Please complete the [Notes for deployment of MD OT Security | Firewall Allow-listed Configurations](/docs/md-ot-security/installation/whitelist-url-for-ot-security)

- Obtain the latest ISO from <https://my.opswat.com/home/metaDefender-ot-security>

## [Procedure](/docs/md-ot-security/installation/iso-esxi-installation#procedure)

1. Log in to the Host Client at https://<ESXI_HOST>/UI.

In this URL, <ESXI_HOST> is the IP address or FQDN of the ESXi host where you want to deploy your virtual machine.

2. Right-click the ESXi host and select **Create/Register VM**.

The Host Client displays the New Virtual Machine window.

3. On the Select creation type page, select **Create a new virtual machine**. → Click **Next**

4. On the Select a name and guest OS, do the following:

   1. In **Name**, type a name for the virtual machine.
   2. In **Compatibility,** keep as default, example: **ESXI 8.0 virtual machine**
   3. In the **Guest OS family**, select **Linux**.
   4. In the **Guest OS version,** select **Debian GNU/Linux 12 (64-bit)**
   5. Click **Next**.

5. On the Select storage page, select an appropriate data storage for your virtual machine and click **Next**.
6. On the Customize settings page, do the following: Configure **Virtual Hardware** tab (CPU, Memory, Disk, NIC, CD/DVD)

   1. In CPU/Memory/Hard disk: follow the requirements for each component [Requirements for deploying MetaDefender OT Security](/docs/md-ot-security/installation/requirements-for-deploying-mdots)
   2. In Network Adapter: the default is 1 NIC, click Add network adapter and select a mapping suitable for each component (Follow the requirement - [Requirements for deploying MetaDefender OT Security](/docs/md-ot-security/installation/requirements-for-deploying-mdots) )
   3. In **CD/DVD Drive 1,** select the **Datastore ISO file,** then upload the **ISO file just downloaded,** and click Select
   4. At the **VM Options** tab, in Boot Options, select **EFI**
   5. **Click** **Next .**

CPU/Memory/Hard disk

Upload the ISO

7. On the Ready to Complete page, review the virtual machine settings and click **Finish**
8. Power on the VM, then wait until importing completed.
9. Select the component, then wait until the virtual machine is deployed.

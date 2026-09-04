<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/installation/deploying-mdots-site-bundle-ova -->

# Deploying the MetaDefender OT Security Site Manager & Network Sensor - Bundle 2 in 1 OVA using the Host Client connected directly to the ESXi host

## [About this task](/docs/md-ot-security/v.3.4.0/installation/deploying-mdots-site-bundle-ova#about-this-task)

Use this procedure to deploy MetaDefender OT Security Site Manager & Network Sensor - Bundle 2 in 1 OVA on vCenter using the Host Client.

## [Before you begin](/docs/md-ot-security/v.3.4.0/installation/deploying-mdots-site-bundle-ova#before-you-begin)

- Obtain the latest OVA from <https://my.opswat.com/home/metaDefender-ot-security>

## [Procedure](/docs/md-ot-security/v.3.4.0/installation/deploying-mdots-site-bundle-ova#procedure)

1. Log in to the Host Client at https://<ESXI_HOST>/UI. In this URL, <ESXI_HOST> is the IP address or FQDN of the ESXi host where you want to deploy your virtual machine.
2. Right-click the ESXi host and select **Create/Register VM**. The Host Client displays the New Virtual Machine window.
3. On the Select creation type page, select **Deploy a virtual machine from an OVF or OVA file**.
4. Click **Next**.
5. On the Select OVF and VMDK files page, do the following:

   1. In **Name for the virtual machine**, type a name for the virtual machine.
   2. In **Click to select files or drag/drop**, upload the OVA file to the Host Client.
   3. Click **Next**.
6. On the Select storage page, select an appropriate data storage for your virtual machine and click **Next**.
7. On the Deployment options page, do the following:

   1. In **Network mappings**, select an appropriate network.
   2. Click **Next**.
8. On the Ready to Complete page, review the virtual machine settings and click **Finish**.
9. Wait until the virtual machine is deployed.

**Important:**

Do not refresh the browser page while deployment is in progress.

10. To ensure that the virtual machine automatically starts after a hypervisor reboot, right-click your virtual machine and select **Autostart** > **Enable**. If you do not enable autostart, you must manually start the virtual machine when the hypervisor reboots.

**Note:**

You must enable the autostart functionality on the ESXi host for the virtual machine autostart to function.

11. To start the virtual machine, right-click the virtual machine and select **Power** > **Power On**.
12. Access the virtual machine console.

## [Next Steps](/docs/md-ot-security/v.3.4.0/installation/deploying-mdots-site-bundle-ova#next-steps)

- Configuration for Site Manager & Network Sensor - Bundle 2 in 1 on local management console application.

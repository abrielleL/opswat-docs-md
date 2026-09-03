<!-- source: https://www.opswat.com/docs/ocm/operating/remote-install-opswat-products -->

# Remote Install OPSWAT Products

Administrators can install OPSWAT products remotely through the OPSWAT Central Management console. The host machine for the OPSWAT Product must meet the system requirements and have OpenSSH Server enabled.

## [System requirements on an OPSWAT Products' host machine:](/docs/ocm/operating/remote-install-opswat-products#system-requirements-on-an-opswat-products-host-machine)

**Windows:**

- Windows 10 ; Windows Server 2012, 2012 R2 and 2016
- Powershell 5.1 or higher
- OpenSSH Server is enabled on the host machine

**RHEL/Ubuntu:**

- The latest version of RHEL 7.7 or Ubuntu 18.04
- The packages bash, wget (or curl), and openssh-server are installed and enabled on the host machine

Administrators can follow the below steps to install an OPSWAT product on a remote machine through OPSWAT Central Management console. Note that while these steps are demonstrated with the MetaDefender Kiosk product, you can apply the same process for other OPSWAT Products such as MetaDefender Core and Managed File Transfer.

1. Go to the **MetaDefender Kiosk** management page under **Inventory** in the sidebar.

2. Click the **ADD NEW INSTANCE** button in the top right panel.

3. The dialog **Add Kiosk** will be opened. Select the **Remotely install a new Instance** button.

4. Fill the proper inputs and click the **TEST CONNECTION** button to check the connection status.

- **Name:** The name of the new Kiosk instance.

- **Server Address:** The server address of the remoted device.

- Username, Password: The credentials used to access the remoted device.

- **Installer URL:** The URL to download MetaDefender Kiosk.

5. The dialog will be closed and the Kiosk management page will be reloaded automatically if the result is successful.
6. For MetaDefender Kiosk version 4.3.0 and above, a unique API Key is required to connect to OPSWAT Central Management. Log into the remoted device and retrieve the API Key from the User Management menu. Click **Generate** to get the API Key

7. Click on the gear icon in the new kiosk's entry in the Kiosk Management page on your OPSWAT Central Management. Select **Edit**.

8. Enter the new API Key retrieved from step 6 into the API Key entry for MetaDefender Kiosk version 4.3.0 and above. For older versions, please enter "admin".

9. The status of the Kiosk is **Connected** after fetching the version of this Kiosk instance successfully.

TLS compatibility

If you wish to enable TLS protocols for the file server hosting the installation file, please note that the remote installation feature currently only supports TLSv1.2 on Windows host machines (the target machine that should have OPSWAT Product installed).

For TLSv1.3, because PowerShell does not properly provide support for this version on Windows 10 and Windows Server 2012, 2012 R2 and 2016, the remote installation feature won't function correctly.

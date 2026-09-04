<!-- source: https://www.opswat.com/docs/macloud-sdp/metadefender-it-access-on-prem/my-opswat-endpoint-management-installation-guide -->

# MetaDefender IT Access On Prem Installation Guide

#### [Installation](/docs/macloud-sdp/metadefender-it-access-on-prem/my-opswat-endpoint-management-installation-guide#installation)

Before starting MetaDefender IT Access On Prem installation, please make sure your server meets the [minimum system requirement](https://docs.opswat.com/macloud-sdp/configuration---management/recommended-system-requirements).

**Note:** Root access is restricted in OVA-based deployments. For enhanced administrative control and customization, use the MSI installer for Windows Server — [[click here](https://www.opswat.com/docs/cm/deployment/msi-installation)].

## [Installation steps](/docs/macloud-sdp/metadefender-it-access-on-prem/my-opswat-endpoint-management-installation-guide#installation-steps)

1. Download the MetaDefender IT Access On Prem from [My OPSWAT](https://my.opswat.com/home/my-opswat)
2. Deploy MetaDefender IT Access On Prem system by importing this file into [virtualization systems](https://docs.opswat.com/macloud-sdp/metadefender-it-access-on-prem#software-version).
3. The configuration wizard will walk you through the basic setup of MetaDefender IT Access On Prem.
4. After installation is finished, you can access the MetaDefender IT Access On Prem console via the address [http://<*your server ip address>/*](http://your-server-address)

Notes: You will need to enable "3D support" from VMWare: Navigate to the 'Video Card' section in the VM instance settings and make the necessary adjustments

## [Configuration wizard](/docs/macloud-sdp/metadefender-it-access-on-prem/my-opswat-endpoint-management-installation-guide#configuration-wizard)

After importing the OVA into vCenter and starting the virtual machine, wait for 2-3 minutes as the system initializes and starts the underlying infrastructure.

After the system finishes booting, initiate the installation process by selecting from the following options:

- **New Setup**: For new installations.​
- **Restore from Backup**: In case administrators want to restore the system from a backup file.

## [Setting up wizard with the new setup.](/docs/macloud-sdp/metadefender-it-access-on-prem/my-opswat-endpoint-management-installation-guide#setting-up-wizard-with-the-new-setup)

Step 1: The first step is for the customer to read and agree to the OPSWAT Inc. Terms of Service and Privacy Policy.

Step 2: Provide admin user information including first name, last name, email, and password.

Step 3: View and modify the system's IP address if needed.

Step 4: Server Settings:​

- **Server URL:** Admins can access the MetaDefender IT Access console using this URL.

**MetaDefender Endpoint Recovery Key**: This key establishes the connection between MetaDefender IT Access and MetaDefender Endpoint.

- Choose one of the following options:

  - Generate a new key: for new installation​.
  - Use existing key: If you had a previous MetaDefender IT Access setup.

Step 5: Related to licensing, supports both online and offline activation modes. Skip this step if admins don't have a key.

Step 6: Summary step - Admin can review all information, including Administrator User, Server Configuration, IP Settings, and License. To make edits, the admin can use the back button or click on the left menu to navigate to the desired section.

If all information is correct, click 'Continue,' and the system takes 2-3 minutes to complete the installation process

After completing setup, the system will redirect to the login page. Enter admin email and password to access the MetaDefender IT Access On Prem Console.

The MetaDefender IT Access On Prem Console, like the MetaDefender IT Access version, includes features such as the dashboard and inventory... Additionally, it offers specific functionalities like Backup, User Management, Server Config, License, and Support Package.

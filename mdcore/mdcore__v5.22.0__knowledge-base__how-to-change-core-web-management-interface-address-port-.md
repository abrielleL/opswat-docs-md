<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-change-core-web-management-interface-address-port- -->

# How to change Core Web Management Interface Address Port?

By default, MetaDefender Core’s Web Management Interface is available via Port 8008.

This is customizable via Registry Editor in Windows and /etc/ometascan/ometascan.conf file in Linux.

To change the port, you can follow the steps below:

## [Windows:](/docs/mdcore/v5.22.0/knowledge-base/how-to-change-core-web-management-interface-address-port-#windows)

1. Press **Win+R**, type **regedit** and press Enter to open **Registry Editor**:

2. Navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\global**, select **restport** Key and select **Modify…**

3. Enter the desired port and click the **OK** Button

4. Open a **Command Prompt** as an **Administrator** and run the following commands to restart **MetaDefender Core** **Service**:

Command PromptCopynet stop ometascan
net start ometascan

5. You can now access the **MetaDefender Core** **Web Management Interface** via configured **Port**:

## [Linux:](/docs/mdcore/v5.22.0/knowledge-base/how-to-change-core-web-management-interface-address-port-#linux)

1. Open the /etc/ometascan/ometascan.conf file in edit mode:

ExampleCopysudo vim /etc/ometascan/ometascan.conf

2. Edit the **restport** value with the desired port:

3. Save the changes and restart the **MetaDefender Core Service** using the following command:

BashCopysudo systemctl restart ometascan

4. You can now access the **MetaDefender Core** **Web Management Interface** via configured **Port**:

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).

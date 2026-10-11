<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/advanced-deployment/kiosk-application-deployment-via-sccm -->

# Kiosk application deployment via SCCM

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This document provides instructions to setup Microsoft Configuration Manager (SCCM) for Kiosk deployment. This guide is based on Microsoft Configuration Manager version 2403 (5.00.9128.1000), installed on Windows Server 2022 Standard 21H2 (OS Build 20348.1970)

## Prerequisites

Before starting the setup process, make sure your environment meets requirements:

- Domain Controller (DC) machine for domain joining.
- The Configuration Manager (CM) machine with SCCM installed.
- The client machine and the CM machine must be joined to the same domain.
- [For the Kiosk upgrade] The client machine already has a version of Kiosk installed.

## Kiosk application deployment via SCCM

**Step 1.** Make sure SCCM Client already installed on Client machine

- From SCCM console, navigate to "Assets and Compliance" → "Devices". The "Client" column of the device should be marked as "Yes"

- If not, right-click the device and select Install Client. This option will install the SCCM client on the client machine.

Info

Adding the Kiosk device to the SCCM and Installing SCCM Client to the device are out of the scope of this guide.

**Step 2.** Download and prepare Kiosk installer

- Download the Kiosk application via [My OPSWAT portal](https://my.opswat.com/)
- Copy the Kiosk installer (MetaDefender_Kiosk_ <version>.exe) to the network share folder of on the SCCM server (e.g &lt;hostname>\SMS_<sitecode>)

**Step 3.** Configure application on SCCM console

- Log in to the **Configuration Manager Console** using administrator credentials.
- Navigate to **Software Library** → **Overview** --> **Application Management** → **Applications**
- Right click on the white space to **Create Applications**

- Because Kiosk Installer is an .exe (not .msi), so we need to manually set up the application information by choosing **Manually specify the application information** on the appeared pop up.

- Name the Application, then configure your **Deployment Types** of this application.

  - Select **Add** to add new deployment types for your application with manual config by script installer.

- The Kiosk application will be installed by command line, so we need to configure the command to run the installer. On the Content windows, configure the following

  - **Content Location:** The path of the installer
  - **Installation program:** by “<your exe installer>” /quiet and Uninstall program by “<your exe installer>” /uninstall /quiet . For example: “MetaDefender_Kiosk_ 4.7.10.4379.exe” /quiet, “MetaDefender_Kiosk_4.7.10.4379.exe” /uninstall /quiet Note: /quiet mode is required because we cannot install Kiosk to other agent with manual options. Moreover, we need to have the installer for each agent, so we suggest to place your installer on shared network.

- For the **Detection Method**, this is the way that system detects if your application is successfully deployed on agent, on Kiosk, we will detect it by checking the specified registry, which is set after an installation or upgrade process. Add Clause and configure Registry in hive HKEY_LOCAL_ MACHINE, path SOFTWARE\WOW6432Node\OPSWAT\MD4M, value version, load it as String value and check if it is equal to to-upgraded version as detection type.

- After configure Deployment Types, you can exit and check out your Create Application progress and your added application will be visible on the Applications list.

**Step 4**. Deploy Kiosk application

- Log in to the **Configuration Manager Console** using administrator credentials.
- Right click on the to-deployed application, select **Deploy**.

- Configure Collection to target the upgrade group on your domain.

- If collection not created yet, go to the **Assets and Compliance → Device Collections**, create the collection.

- Add **Direct Rule** and click **Next.**

- On the next page, configure the points that will host this deployment by **Add → Distribution Point**

- Configure your **Deployment Settings, Scheduling, User Experience** and **Alerts** if needed.
- View the summary again to verify your setting and Deploy this application to agent in specified group. The installation scheduler in each agent will start after new policy from the SCCM applied.

**Step 5.** Verify Installation

- On the CLIENT agent, open Software Center.

- Check if the added Kiosk application is listed and installed.

- Launch the Kiosk app to confirm successful deployment.

**Step 6.** Configure the initial setup for Kiosk

- For the fresh installation of the Kiosk, navigate to http://<Kiosk-IP-address>:8009 to continue the Kiosk application initialization - [Configuring the Management Console for initial use - MetaDefender Kiosk Windows](https://www.opswat.com/docs/mdkiosk/installation/configuring-the-management-console-for-initial-use)

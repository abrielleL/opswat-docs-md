<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/advanced-deployment/setup-rfid-card-for-user-authentication -->

# Setup RFID card for user authentication

## [Overview](/docs/mdkiosk/v4.8.5/advanced-deployment/setup-rfid-card-for-user-authentication#overview)

This guide demonstrates the prerequisites and process of setting up an RFID Smart Card reader for authentication in MetaDefender Kiosk. Please note that this guide is for reference only. For the most accurate instructions, refer to the setup documentation provided by your Smart Card providers.

## [Prerequisites](/docs/mdkiosk/v4.8.5/advanced-deployment/setup-rfid-card-for-user-authentication#prerequisites)

**RFID Card Reader**

MetaDefender Kiosk supports integration with RFID Smart Card readers in keyboard emulation (or wedge) modeand are configured to terminate output with an <Enter>. Most common card readers that can be configured to meet these prerequisites should work with Kiosk. We have specifically tested with the following models:

- DUALi DE-620 RF card reader
- ELATEC TWN4 MultiTech 2 LF HF RFID reader

Quick tips to check if the RFID Card Reader compatibility with Kiosk

1. Connect the RFID card reader to a PC and open Notepad. Ensure the cursor is active in Notepad
2. Swipe the card. If a number appears (ending with <Enter>), the card is using HID
3. Swipe the card again. If the same number appears on a new line, the card is supported

**Active Directory**

MetaDefender Kiosk requires a connection to an Active Directory server in order to authenticate and map users to their RFID card. A field in Active Directory must be made available and Kiosk granted the appropriate permissions to write to that field in order to maintain the mapping.

## [Integrate with AD and Enable RFID authentication](/docs/mdkiosk/v4.8.5/advanced-deployment/setup-rfid-card-for-user-authentication#integrate-with-ad-and-enable-rfid-authentication)

- From **Kiosk WebMC**, navigate to **Workflows**, under **Employee Workflow**, click on **Set Default Login Method**, select **MetaDefender Kiosk Authentication**, select **Remote Active Directory.**

  - Click on **Add new** and provide the information of your Active Directory server for integration

- Click on **Enable RFID authentication**. Provide the information below:

  - **Reader vendor ID**: RFID reader vendor ID can be found in the Device Manager (see the steps)
  - **Mapping field name in AD**: Provide a custom field in AD user attributes to store RFID card code. If not provided, Kiosk uses EmployeeID by default

### [Acquire RFID reader vendor ID](/docs/mdkiosk/v4.8.5/advanced-deployment/setup-rfid-card-for-user-authentication#acquire-rfid-reader-vendor-id)

- Press **Win + R**, type **devmgmt.msc**, and open it with Administrator permissions

- Under **Device Manage**r, navigate to **Keyboards,** plug in the RFID reader to the Kiosk system. The first **HID Keyboard Device name** should be the RFID reader

- Double-click on **HID Keyboard Device ID**. It should pop up a properties window, click on **Details** tab, change **Property** to **Device instance path** to verify the value.

  - You should see the value similar as the example below. **Reader vendor ID** is the 4 characters after "VIC_", in this example, it is **09D8**

### [Mapping field name in AD](/docs/mdkiosk/v4.8.5/advanced-deployment/setup-rfid-card-for-user-authentication#mapping-field-name-in-ad)

- Open **Active Directory User and Computers** and select **Properties** of a user. Go to **Attribute Editor** tab, you can use any available attribute for Kiosk to set RFID card code. For example, **uid**

## [Swipe the RFID card to login](/docs/mdkiosk/v4.8.5/advanced-deployment/setup-rfid-card-for-user-authentication#swipe-the-rfid-card-to-login)

Once the configure is completed, end user will be able to login using a registered RFID card

## [Kiosk Users register RFID cards](/docs/mdkiosk/v4.8.5/advanced-deployment/setup-rfid-card-for-user-authentication#kiosk-users-register-rfid-cards)

If the RFID card is not registered on the AD Server, the user can register it by themselves

- In the **Kiosk UI**, select **Employee Workflow** and login with an AD account
- At the **Insert media** screen, the user can register the RFID card if it is not yet registered, Click on **... icon** to access more settings, click on **Active** button next to **RFID tags**

- Kiosk will request the user to swipe a RFID card for registration

- When successfully register an RFID card, Kiosk will show the screen below

- The user can verify if their RFID card is registered to their account by clicking on **... icon** to access more options. If the card is registered, Kiosk will display **Activated** next to **RFID tags**. Once activated, the user can authenticate to Kiosk simply by swiping their RFID card

<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/secure-image/metadefender-kiosk-secure-image-deployment -->

# MetaDefender Kiosk Secure Image Deployment

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Step 1: Boot into Secure Image flash-drive](/docs/mdkiosk/v4.8.6/secure-image/metadefender-kiosk-secure-image-deployment#step-1-boot-into-secure-image-flash-drive)

If you don't have the Secure Image flash-drive ready, please follow [Creating Secure Image Deployment flash drive](/docs/mdkiosk/v4.8.6/secure-image/creating-deployment-usb)

1. Plug USB into **Kiosk Hardware**.
2. Restart/Power on the device.
3. Keep pressing **F12** during booting up to open **Boot Menu**
4. Select the created USB as boot up media (base on device name)
5. Press **Enter**.

Boot Menu from the Kiosk K1001 (Dell 7410)

## [Step 2: Deploy Secure Image](/docs/mdkiosk/v4.8.6/secure-image/metadefender-kiosk-secure-image-deployment#step-2-deploy-secure-image)

- Following the boot into the WinPE environment, the Deployment Wizrd will appear.

You can see the Image information and click **Next** button to continue to the next step.

- Choose the disk to apply the image on the next screen.

Warning

Make sure that you choose the right disk in this step. The selected disk will be erased for installation

- Choose the desired options, then click the SUBMIT button to start the installation.

- The process will be processed automatically.

## [Step 3: Post Deployment Actions](/docs/mdkiosk/v4.8.6/secure-image/metadefender-kiosk-secure-image-deployment#step-3-post-deployment-actions)

- Change default log-in information for the local windows account:

  - **Username**: KioskUser
  - **Password**: Contact the Customer Support to get the default password.
- To activate MetaDefender Core, you will need to run the **Setup Wizard** on MetaDefender Core, as follows:

  - Go to [http://localhost:8008](http://localhost:8008/) and follow the **Wizard** in order to create an account and activate MetaDefender Core.
- To activate MetaDefenderKiosk, you will need to run the **Setup Wizard** on MetaDefender Kiosk, as follows:

  - Go to <http://localhost:8009/> and follow the **Wizard** in order to create an account and activate MetaDefender Kiosk.
- Connect Kiosk to MetaDefender Core by following the instructions [Here](https://docs.opswat.com/mdkiosk/configuration/configuring-with-metadefender-core).
- Change MD Core Database credential:

From MD Core console, navigate to Settings > Network > Database > Configure

Enter a new password, check the option “Also change password on Postgres Server”

Warning

A PIN code is required for this step. If you haven't setup the PIN code, please set up a PIN code.

Support:

If you have followed the instructions above but are **Unable To Install And Run MetaDefender Kiosk Using A Bootable Kiosk Flash Drive**, please log a [Support Ticket](https://www.opswat.com/support) with the OPSWAT team.

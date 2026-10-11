<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-to-remotely-shutdown-or-restart-the-system-from-the-kiosk-ui -->

# How to remotely Shutdown or Restart the System from the Kiosk UI?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Starting with **MetaDefender Kiosk version 4.7.3**, administrators can remotely restart or shut down a Kiosk machine directly from the **MetaDefender Kiosk Management Console**. This feature is particularly useful for managing remote deployments without requiring physical access to the Kiosk machine.

**Important Note:** If your machine is configured to require a login (e.g., Windows login), restarting the system will stop at the login screen. An administrator will need to log in locally or through a remote management solution to complete the boot process.

**Restarting or Shutting Down the Kiosk**

1. In the **Device Information** view, you will see **System** or **Network Interface Information** details
2. Look for the buttons labeled:

   1. **Restart System**
   2. **Shutdown System**
3. Click the relevant button to initiate the desired action:

   1. **Restart System:**

      1. Triggers a standard Windows restart.
      2. If the machine is configured with a login prompt, it will require manual login after reboot.
   2. **Shutdown System:**

      1. Powers down the Kiosk machine entirely. You will need physical access or remote power management to turn it back on.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

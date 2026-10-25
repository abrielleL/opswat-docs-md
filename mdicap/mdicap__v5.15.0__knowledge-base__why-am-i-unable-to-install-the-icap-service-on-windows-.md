<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/why-am-i-unable-to-install-the-icap-service-on-windows- -->

# Why Am I Unable to Install the ICAP Service on Windows?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info:

This article provides solutions and workarounds for resolving installation failures of the MetaDefender ICAP Server.

Error:

Error message: Service ‘OPSWAT MetaDefender ICAP Server’ (mdicapsrv) could not be installed. Verify that you have sufficient privileges to install system services.

If you encounter an issue while installing the MD ICAP service from the MSI file and observe the following error:

In the Event Viewer, you will find an error log from the MSI event similar to the following:

Check the details of the error event for more information.

The **Error 1923** in MetaDefender ICAP Server installation usually indicates a **permissions issue** preventing the service (`mdicapsrv`) from being installed as a system service. Here are some troubleshooting steps to resolve this:

#### [**1. Run the Installer as Administrator**](/docs/mdicap/v5.15.0/knowledge-base/why-am-i-unable-to-install-the-icap-service-on-windows-#1-run-the-installer-as-administrator)

- Right-click on the MetaDefender ICAP Server installer (`.exe` or `.msi`).
- Select **"Run as administrator"**.
- Proceed with the installation.

#### [**2. Check for an Existing mdicapsrv** **Service**](/docs/mdicap/v5.15.0/knowledge-base/why-am-i-unable-to-install-the-icap-service-on-windows-#2-check-for-an-existing-mdicapsrv-service)

The installer might be failing because a previous installation left an incomplete service. Check if the service already exists:

1. Open **Command Prompt** as Administrator.
2. Run:

PowershellCopysc query mdicapsrv

3. If the service exists as output below

4. Try removing it with administrator privileges using the following command:

PowershellCopysc delete mdicapsrv

5. If you notice the following output:

This means that the service has already been marked for deletion and is awaiting an OS reboot. You can restart or reboot your machine and then proceed with reinstalling the MD ICAP service.

After rebooting or restarting the OS, the `mdicapsrv` service will be completely removed. You can verify this by running the command mentioned in step 2.

Now, you can install MetaDefender ICAP Server again.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

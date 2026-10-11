<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-getting-an-insufficient-user-rights-error-when-updating -->

# Why Am I Getting an Insufficient User Rights Error When Updating Kiosk?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

When attempting to update the Kiosk application, you may encounter an error message during the installation process related to **insufficient user rights**. This typically occurs when certain Windows features required by the Kiosk app are not enabled on the system.

**Cause**:

The error often appears when the Wireless Networking feature is not enabled in the Windows environment. This can prevent necessary services from running properly during the update process.

**Solution**:

To resolve the issue, you need to manually enable the Wireless Networking feature using the DISM tool.

Step-by-Step Instructions:

1. Open Command Prompt as Administrator:

- Click Start, type cmd
- Right-click on Command Prompt and choose Run as administrator

2. Run the following command:

**dism /online /enable-feature /featurename:WirelessNetworking /all**

- This command enables the Wireless Networking feature and any required dependencies.

3. Restart your system (if prompted).
4. Try updating the Kiosk application again.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

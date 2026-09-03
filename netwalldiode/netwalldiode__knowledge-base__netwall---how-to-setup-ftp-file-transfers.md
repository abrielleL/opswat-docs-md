<!-- source: https://www.opswat.com/docs/netwalldiode/knowledge-base/netwall---how-to-setup-ftp-file-transfers -->

# NetWall - How to setup FTP File Transfers

**Prerequisites**

- **Device Readiness:** Ensure your NetWall Diode appliance is powered on, connected, and that any required security dongles are properly inserted.
- **Network Connectivity:** Verify that the diode and the FTP server have network connectivity.
- **Credentials:** Have your FTP server details (IP/hostname, port, username, password, and file path)

**Step-by-Step Configuration**

1. Log In to the Management UI

- Open your preferred web browser.
- Navigate to the management IP address of your NetWall Diode.
- Enter your user credentials to access the management interface.

2. Access the File Transfer Section

- From the main dashboard, select **File Transfer** from the navigation menu.
- The File Transfer section will list the supported file transfer protocols.

3. Select the FTP Option

- Click on the **FTP** label to display the FTP-specific configuration options.
- Click the **Add FTP Share** button to begin creating a new FTP file transfer profile.

4. Configure FTP Settings

- **Server Details**: Enter the FTP server’s IP address or hostname and port number (default is 21 unless a custom port is used).
- **Credentials:** Input the FTP username and password required to access the server.
- **File Path:** Specify the directory or file path on the FTP server where the files are located.
- **Additional Parameters:** Configure any optional settings such as connection timeout or choose between active and passive transfer modes based on your network requirements.

5. Save and Validate the Configuration

- Click **Save** to apply your FTP settings.
- (Optional) Use the **Test Connection** feature to verify that the NetWall Diode can establish a successful connection to the FTP server.

**Additional Considerations**

- **One-Way Transfer Enforcement:** The NetWall Diode is designed to enforce unidirectional data flow. Once configured, files will transfer from the external FTP share into the secure network without a return path.
- **Security Best Practices:** Ensure that the FTP server is hardened and configured to allow only the necessary one-way transfers.
- **Monitoring & Logs:** Regularly check the device logs within the management UI to verify successful transfers and to troubleshoot any issues.

**Troubleshooting**

- **Connection Issues:**

  - Confirm that the FTP server’s IP address, port, and credentials are correct.
  - Verify that network firewalls permit FTP traffic from the diode’s external interface.
- Transfer Failures:

  - Ensure that the specified file path exists and that the FTP user has read permissions.
  - Review any error messages in the management UI logs for clues.

By following the above steps, you should be able to successfully configure FTP file transfer on your OPSWAT NetWall Diode, ensuring secure and compliant one-way data transfer between networks.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

MetaDefender

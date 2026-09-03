<!-- source: https://www.opswat.com/docs/mdtransferguard/configuration/10-advanced-menu -->

# Advanced Menu

The **Advanced** menu allows administrators to run diagnostic tests, view and update configuration information.

## <Diagnostics>

Use the **Diagnostics** menu options to run tests on Diode X.

### [Ping Test](/docs/mdtransferguard/configuration/10-advanced-menu#ping-test)

Click the **Ping Test** option to run a ping test. Enter the server IP address or hostname in the **Target Address** box and click the **Submit** button. The results from the ping are displayed.

### [TCP Connect](/docs/mdtransferguard/configuration/10-advanced-menu#tcp-connect)

Click the **TCP Connect** option to view the result of the handshake between the client and the server that’s listening.

1. Enter an IP address or hostname in the **Target Address** box.
2. Enter a port number (required).
3. Click the **Submit** button. The handshake results display.

### [Show Route](/docs/mdtransferguard/configuration/10-advanced-menu#show-route)

Click the **Show Route** option to view the route the packet took to get to its destination. Enter an IP address or hostname in the **Target Address** box and click the **Submit** button. The route displays.

### [Trace Route](/docs/mdtransferguard/configuration/10-advanced-menu#trace-route)

Click the **Trace Route** option to display the route and time the packet took to get to its destination. It will do a maximum of 30 hops at 60 bytes per packet. Enter an IP address or hostname in the **Target Address** box and click the **Submit** button. The route and time display.

### [DNS Lookup](/docs/mdtransferguard/configuration/10-advanced-menu#dns-lookup)

Click on the **DNS Lookup** option to list DNS records for a domain. Type the target address or domain and click submit to obtain the list.

### [Login Attempts](/docs/mdtransferguard/configuration/10-advanced-menu#login-attempts)

Click the **Login Attempts** option to view the following information about locked-out users and unlock a user account (times shown are the appliance system time):

- **Name**: All users locked out of the appliance.
- **IP**: IP address that attempted to connect to the appliance
- **Failed Attempts**: Number of times the user tried to log on
- **Last Failed**: Last time the user tried to log on
- **Locked**: Time the system locked the user out
- **Action**: Procedures you can perform for this user

Select the user, open the **Action** menu, and click **Clear** to unlock the account for that user.

### [Login Lockout](/docs/mdtransferguard/configuration/10-advanced-menu#login-lockout)

Click the **Login Lockout** option to set the maximum amount of login tries before the system locks the account.

The login lockout prevents unauthorized users attempting brute-force attacks. The default number for login lockout is three.

If your authorized users frequently log on incorrectly, the root cause should be identified and correct . It is not recommend to address by increasing the login lockout number.

1. Enter the maximum number of login attempts before the system locks the account in the **Max Failed Attempts** box.
2. Enter the number of minutes the system keeps the account locked in the **Locked Duration** box.
3. Click the **Submit** button. A green banner at the top of the page tells you the procedure succeeded.

To return MetaDefender Diode X to default values, open the **Action** menu and click **Reset to Default Configuration.**

To see users who are locked out of their accounts, open the **Action** menu and click **Manage Locked Accounts**. The *Login Attempts* page opens.

### [Support Package](/docs/mdtransferguard/configuration/10-advanced-menu#support-package)

For troubleshooting purposes, a "Support Package" can be generated to include all relevant configuration and system logs. The Support Package can be sent to OPSWAT Customer Support to expedite issue resolution.

Important

For most support issues, the OPSWAT customer support team will request that users provide a Support Package so it is highly recommended that they are provided with the initial customer support request.

To generate the support package:

1. Go to **Advance -> Diagnostics -> Support Package**.
2. If the user wants to encrypt the file, check Encrypt Package box.
3. Include the password to decrypt the file.
4. Confirm the Password.
5. Optionally, add a comment.
6. Click on Generate button.

### [IP Tables Info](/docs/mdtransferguard/configuration/10-advanced-menu#ip-tables-info)

You can check the information related with the IP tables in the system by clicking in Advanced-> Diagnostic -> **IP Tables Info.**

## <Networking>

Use the **Networking** options to view information about interfaces, IP addresses, and L3 Routes for the Transfer Guard server.

### [Add L3 routes](/docs/mdtransferguard/configuration/10-advanced-menu#add-l3-routes)

You can add new L3 routes in Networking menu inside Advanced menu.

1. Go to **Advanced-> Networking-> L3 Routes**.
2. Deploy **Action** button and click on Add L3 Route.
3. Fill in Target Range for the L3 route.
4. Fill in Gateway IP
5. Click on **Submit** button to save the changes

### [Remove L3 routes](/docs/mdtransferguard/configuration/10-advanced-menu#remove-l3-routes)

You can remove L3 routes in Networking menu inside Advanced menu:

1. Go to **Advanced-> Networking-> L3 Routes**.
2. Click on the L3 route you want to remove.
3. Deploy **Action** menu and click on **Delete**.
4. Confirm your selection in the pop up.

## [SNMP](/docs/mdtransferguard/configuration/10-advanced-menu#snmp)

Use the SNMP menu to manage monitoring NetWall devices using the SNMP protocol. To add an SNMP System Manager to your Diode X follow the steps:

1. Once in SNMP menu, deploy Action button and click on Add System Manager $plugin[90gg3x2326b]
2. Fill in the following fields:

   1. **Source Address Range:** IPV4 address (including the mask) indicating the source address range we want to monitor.
   2. **Description:** User friendly description for the defined system manager.
   3. **Community String:** Hidden string for the system manager.
   4. **SNMP MIB-2 MIBS:** Tick the corresponding checkbox depending on system manager's Management Information Base.
   5. **UCD MIBS:** Tick the corresponding checkbox depending on the UCD Management Information Base you want to expose.
   6. **OPSWAT MIBS**: Tick the corresponding checkbox depending on the OPSWAT Management Information Base you want to expose.
   7. **Enabled:** Tick this checkbox to enable/disable the System Manager. $plugin[ndwnfq7xpi6]
3. Click on **Submit** to save the changes.

## <Encryption>

Use the **Encryption** options to view and update SSL/TLS credentials and X509 certificates associated with the Diode X server.

### [SSL/TLS Credentials](/docs/mdtransferguard/configuration/10-advanced-menu#ssltls-credentials)

Click the **SSL/TLS Credentials** option. The *SSL/TLS Credentials* pane displays. Use the **Action** menu to perform one of the following:

- Create a local keypair
- Import a keypair
- Set an SSL key

You can update an existing credential by selecting it, then using the **Action** menu on the resulting detail pane to:

- Add, edit, export or delete an individual certificate
- Delete all associated certificates

#### [Self-Signed Certificate](/docs/mdtransferguard/configuration/10-advanced-menu#self-signed-certificate)

To create a self-signed certificate:

- Deploy Action menu and select Create a local keypair
- Fill in the form
- Check the **Self Sign Certificate** checkbox and select the expiration period in the dropdown list
- Click on Submit

### [X509 Certificates](/docs/mdtransferguard/configuration/10-advanced-menu#x509-certificates)

Click the **x509 Certificates** option. The *X509 Certificates* pane displays. Use the **Action** menu to import an X509 certificate.

## <Statistics>

Use the **Statistics** options to view information on **Processes, File System Usage, Memory Statistics and** **System Counters**.

<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/configure-radius-server-for-direct-authentication -->

# Configure RADIUS Server for Direct Authentication

## [Step-by-step guide](/docs/manac/nac-v8.1.1/configuration/configure-radius-server-for-direct-authentication#step-by-step-guide)

Click on “RADIUS Mode” (step 1) to activate configuration mode and then select “Authentication and Enforcement” (step 2).

Step 1: Enable Configuration, Step 2: RADIUS Server

- In the top section of the RADIUS server configuration, set the following values:

  - **Name:** (step 3) A label to help describe this RADIUS server.
  - **Mode:** (step 4) Direct
  - **Authentication Type:** (step 5) EAP-PEAP or MAC authentication only. MAC authentication should only be chosen if for Open and PSK wireless networks and wired ports that are not configured for 802.1x.

Step 3: Name, Step 4: Mode, Step 5: Authentication Type

- Under "Vendors", click the green add icon to add your wireless vendor. If your vendor is not listed, choose “Custom”.

Select a Vendor Drop down

- Under “Active Directory Connection Information” enter all values to match your AD infrastructure. After entering all values, click “Join” to complete the authentication setup.
- **Domain:** The full domain of your Active Directory environment (examples: com, [sub.domain.net](http://sub.domain.net/), domain.local).
- **Workgroup:** This is the workgroup name of your domain. The system will try to derive this from the domain, however, this will not always be accurate. If the default does not work, please confirm the correct value.
- **NetBIOS Name:** This is the name NAC will use as the machine name when it registers itself in Active Directory.
- **AD FQDN:** The FQDN of the domain controller that NAC will authenticate against.
- **User Name:** The username of a Domain Admin or other user with rights to join devices to the domain.
- **Password:** The password corresponding to the given username.
- **DNS IP:** The IP of your specific DNS server that will successfully resolve the AD FQDN to your domain controller.
- After joining the domain, confirm the process was successful by entering test user credentials. The test user can be any user in Active Directory.

<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/configuring-windows-gpo-for-802-1x-wired-authentication--eap-ttl -->

# Configuring Windows GPO for 802.1X Wired Authentication (EAP-TTLS with PAP)

This guide walks through the process of using Group Policy to enable the Wired AutoConfig service, configure the 802.1X supplicant for EAP-TTLS with PAP as the inner authentication method, and trust the RADIUS server certificate on domain-joined Windows machines.

---

## Prerequisites

- Active Directory domain environment with Group Policy management access
- A working "MD NAC Enforcer" or "MD NAC Edge" VM (the RADIUS server)
- The RADIUS server's root CA certificate exported as a .cer or .crt file (Base-64 or DER encoded)
- Domain machines running Windows 10/11 or Windows Server 2016+
- Administrative access to the Group Policy Management Console (GPMC)

---

## Overview of the Configuration Steps

1. Import the RADIUS server CA certificate into Group Policy
2. Enable the Wired AutoConfig service via GPO
3. Configure the 802.1X wired authentication profile for EAP-TTLS with PAP
4. Link the GPO to the appropriate Organizational Unit (OU)
5. Verify the configuration on client machines

---

## Step 1: Obtain and Prepare the RADIUS Server Certificate

Before configuring Group Policy, you need the root CA certificate that signed your RADIUS server's TLS certificate. This is critical — without it, clients cannot validate the RADIUS server's identity during the EAP-TTLS outer tunnel negotiation.

### Exporting the Certificate

If your RADIUS server uses a certificate signed by an internal CA, export the **root CA certificate** (not the server certificate itself) from your Certificate Authority.

- Open the Certification Authority MMC snap-in on your CA server.
- Right-click the CA name, select **Properties**, then click **View Certificate**.
- Navigate to the **Details** tab and click **Copy to File…** to launch the export wizard.
- Choose **Base-64 encoded X.509 (.CER)** as the format.
- Save the file to a network-accessible location (e.g., \\dc01\share\radius-root-ca.cer).

If your RADIUS server uses a certificate from a public or third-party CA, obtain the root CA certificate from that provider.

> **Note:** You must distribute the **root CA** certificate, not the RADIUS server's leaf certificate. The trust chain must be complete for EAP-TTLS validation to succeed.

---

## Step 2: Create and Configure the Group Policy Object

### 2.1 Open Group Policy Management

1. Log in to a Domain Controller or a management workstation with RSAT tools installed.
2. Press Win + R, type gpmc.msc, and press Enter to open the Group Policy Management Console.

### 2.2 Create a New GPO

1. In the GPMC tree, navigate to **Group Policy Objects** under your domain.
2. Right-click **Group Policy Objects** and select **New**.
3. Name the GPO descriptively, for example: 802.1X Wired Authentication - EAP-TTLS.
4. Click **OK**.
5. Right-click the newly created GPO and select **Edit** to open the Group Policy Management Editor.

---

## Step 3: Import the RADIUS CA Certificate via GPO

This step pushes the RADIUS server's root CA certificate to the Trusted Root Certification Authorities store on all targeted machines, allowing them to validate the RADIUS server during EAP-TTLS negotiation.

1. In the Group Policy Management Editor, navigate to: `Computer Configuration   → Policies     → Windows Settings       → Security Settings         → Public Key Policies           → Trusted Root Certification Authorities`
2. Right-click **Trusted Root Certification Authorities** and select **Import…**.
3. The Certificate Import Wizard will launch. Click **Next**.
4. Browse to the root CA certificate file you exported earlier (e.g., radius-root-ca.cer).
5. Ensure the certificate store is set to **Trusted Root Certification Authorities**.
6. Click **Next**, then **Finish**.

The certificate will now appear in the list. When this GPO is applied, every targeted computer will automatically trust this CA.

> **Important:** If your RADIUS server's certificate chain includes intermediate CAs, you must also import those into the **Intermediate Certification Authorities** store using the same method under Public Key Policies → Intermediate Certification Authorities.

---

## Step 4: Enable the Wired AutoConfig Service

The **Wired AutoConfig** service (dot3svc) is disabled by default on most Windows installations. It must be running for Windows to process 802.1X authentication on wired Ethernet interfaces.

1. In the same GPO, navigate to: `Computer Configuration   → Policies     → Windows Settings       → Security Settings         → System Services`
2. In the right pane, scroll down and locate **Wired AutoConfig**.
3. Double-click **Wired AutoConfig** to open its properties.
4. Check the box **Define this policy setting**.
5. Select **Automatic** as the startup mode.
6. Click **OK**.

This ensures the dot3svc service starts automatically on every boot on all machines receiving this GPO.

> **Tip:** You can verify the service is running on a client by opening an elevated Command Prompt and running:
>
> `sc query dot3svc`
>
> The output should show STATE: 4 RUNNING.

---

## Step 5: Configure the 802.1X Wired Authentication Profile

### 5.1 Navigate to Wired Network Policies

1. In the Group Policy Management Editor, navigate to: `Computer Configuration   → Policies     → Windows Settings       → Security Settings         → Wired Network (IEEE 802.3) Policies`
2. Right-click **Wired Network (IEEE 802.3) Policies** and select **Create A New Wired Network Policy for Windows Vista and Later Releases**.
3. Give the policy a name, for example: Corporate Wired 802.1X - EAP-TTLS.
4. Optionally add a description.
5. Ensure **Use Windows Wired Auto Configuration service for clients** is checked.

### 5.2 Configure the Network Authentication Method

1. Switch to the **Security** tab of the new wired network policy.
2. Check **Enable use of IEEE 802.1X authentication for network access**.
3. Click **Properties** next to the selected authentication method to open the EAP-TTLS configuration dialog.

### 5.3 Configure EAP-TTLS Properties

In the EAP-TTLS properties dialog:

#### Outer (Tunnel) Authentication Settings

1. **Enable Identity Privacy**: Check this option and enter anonymous (or leave blank) in the identity field. This sends an anonymous outer identity during the TLS tunnel setup so that the real username is not exposed in the clear.
2. **Trusted Root Certification Authorities**: In the list of trusted root CAs, check the box next to the root CA certificate you imported in Step 3. This tells the supplicant to only accept RADIUS servers whose certificates chain to this specific CA.
3. Optionally, under **Server names**, enter the FQDN of your RADIUS server(s) (e.g., radius.corp.example.com). This adds an additional layer of server identity validation.

#### Inner (Phase 2) Authentication Settings

4. Click **OK** to close the EAP-TTLS properties dialog.

### 5.4 Configure Authentication Mode

Back on the **Security** tab of the wired network policy:

1. Set **Authentication Mode** to **User or Computer authentication** (recommended). This allows authentication during both the login screen (using the machine account) and after user login (using user credentials).
2. Alternatively, choose:
   - **Computer authentication** — authenticates only with the machine account.
   - **User authentication** — authenticates only after a user logs in.
3. Optionally, configure **Maximum Authentication Failures** (default is typically 1).
4. Click **OK** to save the wired network policy.

---

## Step 6: Link the GPO to the Target OU

1. Close the Group Policy Management Editor and return to the GPMC.
2. In the GPMC tree, navigate to the Organizational Unit (OU) that contains the computer accounts you want to target.
3. Right-click the OU and select **Link an Existing GPO…**.
4. Select the GPO you created (e.g., 802.1X Wired Authentication - EAP-TTLS) and click **OK**.

> **Best Practice:** Apply this GPO to a test OU containing a small number of machines first. Verify that authentication works correctly before rolling out to the entire domain.

### Security Filtering (Optional)

If you want to limit the GPO to specific machines within the OU:

1. Select the linked GPO in the GPMC.
2. Under the **Scope** tab, in the **Security Filtering** section, remove **Authenticated Users**.
3. Click **Add** and specify a security group containing only the target computer accounts.

---

## Step 7: Force a Group Policy Update and Verify

### 7.1 Force Group Policy Refresh

On a target client machine, open an elevated Command Prompt or PowerShell and run:

`gpupdate /force`

Then restart the machine to ensure the Wired AutoConfig service starts with the new configuration.

### 7.2 Verify the Wired AutoConfig Service

`sc query dot3svc`

Expected output should include:

`SERVICE_NAME: dot3svc         ...         STATE              : 4  RUNNING         ...`

### 7.3 Verify the Certificate Was Imported

Open a Command Prompt and run:

`certutil -store Root`

Look for your RADIUS root CA certificate in the output. You can also verify via the MMC Certificates snap-in under **Trusted Root Certification Authorities → Certificates**.

### 7.4 Verify the 802.1X Profile Is Applied

Open an elevated Command Prompt and run:

`netsh lan show profiles`

You should see your 802.1X wired profile listed. For more detail:

`netsh lan show settings`

### 7.5 Check the Event Logs

Monitor the following event logs on the client for authentication success or failure:

- **Applications and Services Logs → Microsoft → Windows → Wired-AutoConfig → Operational**
- **Security** log (look for event IDs 5765x related to 802.1X)

On the RADIUS server side, check access logs for Access-Accept or Access-Reject messages to confirm the full authentication exchange is completing.

---

## Troubleshooting

### Common Issues and Resolutions

**EAP-TTLS is not available in the authentication method dropdown** Windows versions prior to 1903 do not include native EAP-TTLS support. Upgrade the client OS or deploy a third-party supplicant. You can check the Windows build by running winver on the client.

**The client fails to validate the RADIUS server certificate** Ensure the full certificate chain (root CA and any intermediate CAs) has been imported via GPO. Verify the certificate has not expired. Confirm the FQDN in the server certificate matches the server name configured in the EAP-TTLS profile. Use certutil -verify on the client to check chain validity.

**The Wired AutoConfig service is not starting** Check for conflicting GPOs that may be setting the service to Disabled. Run gpresult /h gpreport.html on the client and review the HTML report for policy conflicts. Also verify no third-party network management software is interfering with the service.

**Authentication fails with an "Access-Reject"** Confirm the RADIUS server is configured to accept EAP-TTLS with PAP. Verify the user credentials are correct and the account is not locked out. On FreeRADIUS, run in debug mode (freeradius -X) to see the detailed inner-tunnel authentication exchange.

**The 802.1X profile does not appear on the client** Run gpresult /r on the client and confirm the GPO is being applied. Ensure the computer account is in the OU (or security group) targeted by the GPO. Check that the Wired AutoConfig service is running — the profile will not appear if the service is stopped.

---

## Summary of GPO Configuration Paths

---

## References

- [Microsoft: Managing the New Wired Network (IEEE 802.3) Policies Settings](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831813(v=ws.11))
- [Microsoft: Configure EAP Profiles and Settings in Windows](https://learn.microsoft.com/en-us/windows-server/networking/technologies/extensible-authentication-protocol/configure-eap-profiles)
- [Microsoft: Extensible Authentication Protocol (EAP) for Network Access](https://learn.microsoft.com/en-us/windows-server/networking/technologies/extensible-authentication-protocol/network-access)
- [Microsoft: Distribute Certificates to Windows Devices by Using Group Policy](https://learn.microsoft.com/en-us/windows-server/identity/ad-cs/distribute-certificates-group-policy)
- [Microsoft: 802.1X Authenticated Wired Access Deployment Guide](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd348468(v=ws.10))
- [Microsoft: 802.1X Authentication Issues Troubleshooting](https://learn.microsoft.com/en-us/troubleshoot/windows-client/networking/802-1x-authentication-issues-troubleshooting)

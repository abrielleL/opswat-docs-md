<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/advanced-deployment/ivanti-device-control-encrypted-device-integration -->

# Ivanti Device Control Encrypted Device Integration

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This document provides instructions on how to configure a Kiosk device to decrypt and work with Ivanti Encrypted devices

## [Prerequisites](/docs/mdkiosk/v4.8.6/advanced-deployment/ivanti-device-control-encrypted-device-integration#prerequisites)

Before you begin, have the following ready:

- The Ivanti Device Control (IDC) client installer (MSI) and its matching MST transform file, obtained from your Ivanti Device Control server.
- A valid Ivanti license file for the endpoint.
- If your Ivanti server uses one, the public key file (`sx-public.key`) used to establish trust between the client and your server.
- For offline deployment (recommended — see the warning below), no network connectivity between the Kiosk device and the Ivanti Device Control server is required.

### [Prepare and deploy Ivanti client](/docs/mdkiosk/v4.8.6/advanced-deployment/ivanti-device-control-encrypted-device-integration#prepare-and-deploy-ivanti-client)

In order for Kiosk device to decrypt the Ivanti-encrypted device, Ivanti client must be installed on the Kiosk device. Here are the steps to prepare and deploy client using the **offline method**, which does **not require any network connection** between the Kiosk device and the Ivanti Device Control Server

Offline deployment of Ivanti client is recommended

Ivanti Device Control supports two deployment methods for installing the Ivanti client on end devices: online and offline. The **offline method is recommended**, as the **LanmanServer service is disabled by default** on Kiosk Hardened Images for security reasons.

If you choose to deploy the client using the online method, please ensure that the LanmanServer service is re-enabled and the firewall is properly configured.

Note: guidance for the online deployment method is outside the scope of this document.

**Step 1.** Create a new package for deployment

- Open IDAC client Deployment Tool. Change the deployment directory
- New package > choose the client MSI > create package name > click OK
- Confirm the package folder contains, at minimum, the client **MSI** and your **MST** file. If your server requires it, also include the **public key** file (`sx-public.key`), used by the client to establish trust with your server.

**Step 2.** Prepare the package folder

- Import public key (if need) to the package
- Set the license file to the package
- Set the policies from the server
- Confirm that there is a package folder created, with minimum an the client MSI, MST, .lic file and the policies.dat (and, if applicable, the public key file sx-public.key used by the client to establish trust with your server).

- Zip the entire package folder and copy to the machine need to deploy client.

**Step 3.** Copy the .zip and run the install the Ivanti client

- Copy the .zip file to the Kiosk machine, and extract the .zip file
- Run the following with Administrator right:

  - client.exe /exenoui /qn TRANSFORMS=Client.x64.mst /L*v \setupcltsu.log

### [Enable Ivanti device decryption option in Kiosk](/docs/mdkiosk/v4.8.6/advanced-deployment/ivanti-device-control-encrypted-device-integration#enable-ivanti-device-decryption-option-in-kiosk)

**Step 1.** Configure Ivanti Device and Application Control path

- From Kiosk console, navigate to Configuration > Advanced > Scanning
- Provide the Ivanti application path in Ivanti Device and Application Control Path. By default, it is "C:\Program Files\Ivanti\Device and Application Control\Client"

**Step 2.** place the needed files in \OPSWAT\Ivanti\

- A license file (named endpoint.lic) is required to use Ivanti features.
- If the required encryption files to unlock the USB are not embedded on the medium, they should be copied to that path, Kiosk will look up in the same folder for the key.

Note

`%ProgramData%` is a Windows environment variable — typically `C:\ProgramData`. Kiosk looks for the license file and any required decryption key files under `%ProgramData%\OPSWAT\Ivanti\`.

**Step 3.** Scan the Ivanti encrypted device with Kiosk

- Start the Kiosk UI and proceed the scanning with Ivanti encrypted device as usual. Kiosk will prompt for password to decrypt the device. Once provided, you can proceed with the scanning process.

### [Supported Operations](/docs/mdkiosk/v4.8.6/advanced-deployment/ivanti-device-control-encrypted-device-integration#supported-operations)

Once an Ivanti-encrypted USB device is unlocked, Kiosk supports:

- Scanning the device's contents
- Copying files to the device
- Retrieving files onto the device (from MetaDefender Managed File Transfer or from a configured directory source)

Wiping an Ivanti-encrypted device is **not** supported.

This integration supports **password-based ("portable mode") Ivanti encryption only**. Certificate-based Ivanti encryption is not supported.

### [Central Management](/docs/mdkiosk/v4.8.6/advanced-deployment/ivanti-device-control-encrypted-device-integration#central-management)

The Ivanti Device and Application Control Path setting and related configuration are supported under Central Management (CM7, CM8, and CM10/MO) policy delivery, and are preserved across backup/restore and Kiosk upgrades.

### [Additional settings for Air-gapped Environment](/docs/mdkiosk/v4.8.6/advanced-deployment/ivanti-device-control-encrypted-device-integration#additional-settings-for-air-gapped-environment)

Due to the nature of the integration between Ivanti and Kiosk, we will try to run the IDC cmd from Kiosk. This raise the security concern of the file integrity, there for Kiosk will implement a signature check for the `HSDC64Cmd.exe` file before usage

The signature validation include:

- Certificate validation
- File integrity validation

In air gapped environment, when the Kiosk machine never had access to the Internet, certificate check will fail with error: **CERT_TRUST_REVOCATION_STATUS_UNKNOWN**

Sample error log: *IDCMedium.cpp#244 IDCMediumCmd::GetRemovableInfo(): {EEEEF1DE-8DC6-4F04-AA2C-3D5F16D8FF8D} Ivanti device control client executable digital signature is not valid: Invalid digital signature: CERT_TRUST_REVOCATION_STATUS_UNKNOWN;Other error status: 0x1000000;*

__

- Reason: Checking if the cert has been revoked by the CA → Try to access CA's certificate revocation list → Fail to access due to completely offline environment
- How to resolve: Manually download and import the CRL to the local machine.

All CRLs must be installed

All CRLs of all the certificates in the PKI chain must be installed

### [Troubleshooting: unlock fails with a password/key error](/docs/mdkiosk/v4.8.6/advanced-deployment/ivanti-device-control-encrypted-device-integration#troubleshooting-unlock-fails-with-a-passwordkey-error)

If Kiosk shows **"Incorrect password or missing access key <id>.key"** when attempting to unlock an Ivanti-encrypted device, check:

- The password entered is correct for that device.
- If the device's encryption key is not embedded on the device itself, the matching `<id>.key` file exists in the configured key folder under `%ProgramData%\OPSWAT\Ivanti\`.

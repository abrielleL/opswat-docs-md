<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/operating/managing-and-distributing-certificates-from-central-management -->

# Managing and Distributing Certificates from Central Management

If you manage a fleet of MetaDefender Kiosk devices with Central Management, you can import a certificate once and distribute it to one device or to a whole group of devices, instead of uploading it separately on every Kiosk. Once a certificate has been distributed to a device, it becomes available wherever that Kiosk needs a certificate — most commonly to serve its management console over **HTTPS**, or to sign its **media manifest**.

This article covers:

1. Importing a certificate into Central Management and distributing it to Kiosk devices
2. Using a distributed certificate to enable **HTTPS** on a Kiosk device
3. Using a distributed certificate to sign the **Kiosk media manifest**

## [Prerequisites](/docs/mdkiosk/v4.8.5/operating/managing-and-distributing-certificates-from-central-management#prerequisites)

- The Kiosk device (or devices) must be enrolled in Central Management.
- You'll need administrator access to Central Management, and the certificate file you want to distribute (in `.pem`, `.crt`, or `.pfx` format) along with its private key and, if the key is encrypted, its passphrase.
- To distribute a certificate to a group of devices at once, you'll also need a **Peripheral Media** policy already set up for that group.

## [Importing a certificate into Central Management](/docs/mdkiosk/v4.8.5/operating/managing-and-distributing-certificates-from-central-management#importing-a-certificate-into-central-management)

1. In Central Management, go to **Settings > Certificates**.
2. Click **Import Certificate**.
3. Enter a name for the certificate, upload the certificate file, upload its private key, and enter the passphrase if the key is encrypted.
4. Save. The certificate now appears in the certificate list.

## [Distributing a certificate to a single Kiosk device](/docs/mdkiosk/v4.8.5/operating/managing-and-distributing-certificates-from-central-management#distributing-a-certificate-to-a-single-kiosk-device)

1. Open the certificate's details page and select **Assign to Instance** from the actions menu.
2. Choose the Kiosk device you want to send the certificate to, and confirm.

To confirm the certificate arrived, open the device under **Inventory > Devices**, select its **Certificates** tab, and check that the certificate appears there. If nothing has been distributed yet, this tab shows "No certificate."

## [Distributing a certificate to a group of Kiosk devices](/docs/mdkiosk/v4.8.5/operating/managing-and-distributing-certificates-from-central-management#distributing-a-certificate-to-a-group-of-kiosk-devices)

If several Kiosk devices share a **Peripheral Media** policy, you can push a certificate to all of them at once instead of assigning it device by device.

1. Open the certificate's details page and select **Assign to Policy** from the actions menu.
2. Choose **Peripheral Media** and select the target policy, then confirm.
3. To have the certificate automatically apply to every device already in the group, open the group under **Inventory > Groups**, go to its **Settings** tab, turn on **Automatically sync group policy for new instance**, and save.
4. For devices that were already in the group before this step, open each device under **Inventory > Devices**, go to its **Settings** tab, and turn on **Apply Group Settings > Automatically sync settings from the group's policy**.

Removing a distributed certificate

If you no longer want a certificate assigned to a device, open the certificate's details page, go to its **Distribution** tab, and choose **Unassign**. If the device can't be reached to confirm the change, use **Force Unassign** instead — this removes the assignment immediately and keeps the certificate available locally on that device rather than deleting it.

## [Using a distributed certificate for HTTPS](/docs/mdkiosk/v4.8.5/operating/managing-and-distributing-certificates-from-central-management#using-a-distributed-certificate-for-https)

Once a certificate has been distributed to a Kiosk device, it becomes available in that device's own **Choose Certificate** setting.

1. Open the device under **Inventory > Devices**, select its **Settings** tab, and choose **Security** from the settings category list.
2. Click **Edit**.
3. Turn on **Enable HTTPS**.
4. From **Choose Certificate**, select the certificate you distributed.
5. Select which TLS versions to allow — **TLS 1.2** and/or **TLS 1.3**. If you don't select either, Kiosk uses its default TLS setting.
6. Click **Save**.

The same fields are available at the policy level (**Peripheral Media** policy > **Settings** > **Security**) if you'd rather configure HTTPS once for an entire group of devices that share a distributed certificate.

## [Using a distributed certificate to sign the Kiosk media manifest](/docs/mdkiosk/v4.8.5/operating/managing-and-distributing-certificates-from-central-management#using-a-distributed-certificate-to-sign-the-kiosk-media-manifest)

The media manifest is a signed record of files processed during a Kiosk session. When Kiosk generates and signs the manifest itself, it uses whichever certificate is set on that device's Security page — so distributing a certificate and setting it up for HTTPS (above) also makes it available for manifest signing.

1. Open the device under **Inventory > Devices**, select its **Settings** tab, and choose **Workflows** from the settings category list.
2. Find the workflow you want to configure and click its edit icon.
3. Select the **Processing** tab.
4. Under **Configuration of scan options**, select **Use MetaDefender Core** — the manifest option is only available for workflows that scan files.
5. In the **Specify the manifest** section, turn on **Enable Media Manifest**.
6. Choose **From MetaDefender Kiosk** so the manifest is generated and signed by the Kiosk itself, using the certificate configured on its Security page.
7. *(Optional, Kiosk 4.8.0 and later)* Turn on **Exclude scan result of original file when its remediated file is available** if you want end users to only see the sanitized version of a file when one exists.
8. Click **Save**.

No separate manifest certificate picker

There's no separate certificate picker just for the manifest feature — it always uses whichever certificate is currently set for HTTPS on that device's Security page. If you want the manifest signed with a different certificate than the one used for HTTPS, distribute and select that certificate on the Security page first.

## [Support](/docs/mdkiosk/v4.8.5/operating/managing-and-distributing-certificates-from-central-management#support)

If you run into trouble managing or distributing certificates from Central Management, please follow the instructions on [How To Create a Support Package](/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-create-a-support-package-for-metadefender-kiosk-) before logging a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team.

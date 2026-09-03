<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-correctly-update-a-certificate-in-metadefender-core- -->

# How to Correctly Update a Certificate in MetaDefender Core?

This article applies to all MetaDefender Core v5 releases deployed on Windows and Linux.

**Introduction**

MetaDefender Core 5.x supports HTTPS connections secured with SSL/TLS certificates. When a certificate approaches its expiration date or needs to be replaced for any other reason, it is important to follow the correct update procedure to avoid service disruption or loss of access to the management interface.

Skipping steps or modifying existing certificate files directly can leave the product in a state where the web UI is unreachable. This article describes the recommended steps for updating a certificate, and provides recovery instructions if the UI becomes inaccessible due to a misconfiguration.

#### [**Update Procedure**](/docs/mdcore/v5.21.0/knowledge-base/how-to-correctly-update-a-certificate-in-metadefender-core-#update-procedure)

Follow the steps below in the exact order listed. Deviating from this sequence may result in loss of access to the management UI.

**Step 1: Add the New Certificate to the Inventory**

Navigate to Inventory > Certificates in the MetaDefender Core management interface and add the new certificate entry with the correct path, file name, and any associated configuration. At this stage:

- Do not modify the existing certificate files in any way.
- Do not replace old certificate files with the new ones on disk.
- The old certificate entry in the inventory must remain untouched until the new certificate has been fully activated.

**Step 2: Enable HTTPS with the New Certificate**

Once the new certificate has been added to the inventory, enable it by navigating to Settings > Security > Secure Connection > Details > Enable Certificate. Select the new certificate from the inventory, fill in all relevant details and options, and save the changes.

Note: Saving the changes will trigger an automatic restart of the MetaDefender Core service to apply the new certificate. Plan for a brief service interruption and notify any affected users accordingly before proceeding.

**Step 3: Remove the Old Certificate from the Inventory**

If the old certificate is no longer needed, remove it from the inventory first. Navigate to Inventory > Certificates, select the old certificate entry, and delete it from there. This step must be completed before deleting or moving the certificate files on disk.

**Step 4: Delete or Move the Old Certificate Files**

Only after the old certificate has been removed from the inventory can you safely delete the certificate files from storage or move them to an archive location. Deleting files before removing the inventory entry can cause startup or configuration errors.

#### [Recovery: Resetting SSL Configuration When the UI Is Unreachable](/docs/mdcore/v5.21.0/knowledge-base/how-to-correctly-update-a-certificate-in-metadefender-core-#recovery-resetting-ssl-configuration-when-the-ui-is-unreachable)

If the steps above were not followed and the management UI is no longer accessible due to a certificate issue, MetaDefender Core provides a command-line utility to reset the SSL configuration back to defaults. Run the appropriate command for your platform.

**Windows**

Run the following executable from an elevated command prompt:

C:\Program Files\OPSWAT\MetaDefender Core\ometascan-reset-ssl-conf.exe

**Linux**

Run the following commands from the terminal:

export LD_LIBRARY_PATH=/usr/lib/ometascan/
/usr/sbin/ometascan-reset-ssl-conf

After running the reset utility, restart the MetaDefender Core service and reattempt to access the management interface. Once access is restored, follow the update procedure described in this article to correctly apply the new certificate.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).

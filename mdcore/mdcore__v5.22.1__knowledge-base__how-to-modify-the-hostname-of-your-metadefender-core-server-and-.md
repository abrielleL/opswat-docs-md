<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-modify-the-hostname-of-your-metadefender-core-server-and- -->

# How to Modify the Hostname of Your MetaDefender Core Server and Potential Impact?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

**Issue**: After updating the hostname of the MetaDefender Core server, the system may experience issues such as Deployment ID changes or difficulties with service operations, certificate validation, and endpoint agent communication.

**Cause**: Changes to the hostname can lead to mismatches in the system certificates and configurations, which might affect the normal functioning of the MetaDefender Core server.

**Solution**:

1. **Disable HTTPS and Remove Current Certificates** : Launch the MetaDefender Core UI, navigate to 'Settings' -> 'Security Tab', click 'Details' under 'Secure Connections', and select 'Do not use certificate'. Save the changes and go to the 'Inventory' -> 'Certificates Tab' to remove the existing certificate.
2. **Deactivate the License** : Go to the 'Settings' -> 'License Tab' in the MetaDefender Core UI. Click on the 'Deactivate License' button. This ensures that your license can be safely transferred to the server once the hostname is changed.
3. **Stop MetaDefender Core Services :**

- For Windows: Open 'services.msc' from the Start menu, locate 'MetaDefender Core Service', and select 'Stop'.
- For Linux: In a terminal window, input 'sudo systemctl stop ometascan' to stop the services.

4. **Rename the Server and Reboot the System** :

- For Windows: Navigate to 'Control Panel' -> 'System and Security' -> 'System' -> 'Advanced system settings'. Under the 'Computer Name' tab, input the new hostname and save changes. Then, restart the server.
- For Linux: In a terminal window, use 'sudo hostnamectl set-hostname [new hostname]' to rename the server, replacing '[new hostname]' with your new hostname. Reboot the server using 'sudo reboot'. Confirm the new hostname with the 'hostname' command.

5. **Reactivate the License** : After changing the hostname and restarting the services, reactivate your license. Go to 'Settings' -> 'License Tab' in the MetaDefender Core UI, and follow the on-screen instructions for license activation. For detailed steps on how to activate the license, please visit [MetaDefender Core Licensing](/docs/mdcore/v5.22.1/installation/metadefender-core-licensing).
6. **Import New Certificate with the New Hostname** : Create a new certificate (PEM or PKCS12 format) with the new hostname. In the MetaDefender Core UI, go to 'Inventory' -> 'Certificates Tab' to add the new certificate. In 'Settings' -> 'Security Tab' -> 'Secure Connections', choose the newly added certificate and save changes. Ensure to import the new certificate into the trusted root certificate store for any endpoint agents or security systems that communicate with MetaDefender Core.

If other systems depend on the MetaDefender Core server's hostname, update their configurations to reflect the new hostname. This might include DNS records, configuration files, or other settings.

Best Practice: Prior to renaming the hostname, it's recommended to test these changes in a non-production environment, ensuring that they conform to your organization's security policies and regulations.

Support:

If you require further assistance, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.1/troubleshooting/how-to-create-support-package-), before logging a [support case or chat with our support engineer](https://my.opswat.com/portal/support).

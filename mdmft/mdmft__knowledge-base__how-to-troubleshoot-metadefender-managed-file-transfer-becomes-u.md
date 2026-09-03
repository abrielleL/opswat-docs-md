<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-to-troubleshoot-metadefender-managed-file-transfer-becomes-u -->

# How to troubleshoot MetaDefender Managed File Transfer becomes unreachable after enabling HTTPS?

Summarize Page    Connect to Cursor Connect to VS Code

This situation is usually caused by a process using the port 80 while NGINX is also trying to use that server. To check if this is true, please follow the below steps:

1. Run the command netstat -np TCP | find ":80" in CMD admin to view the existing processes using port 80
2. Once identified, copy the PID inside the command tasklist.exe /v /fi "PID eq 777", replace 777 with the PID of the process that uses port 80.
3. If the Process is System, then it means that the server has the IIS service installed.

Moving forward, please check if the process identified can be removed or not.

- If the process can be removed, please remove it, and restart the OPSWAT MetaDefender Managed File Transfer Helper, then MetaDefender Managed File Transfer should come up.
- If the process cannot be removed, please follow the below steps:

1. Please navigate to C:\Program Files\OPSWAT\MetaDefender Managed File Transfer\WebServer\conf and open dynamic.conf in a Notepad run as admin.
2. Remove the following lines:

BashCopyserver {
listen 0.0.0.0:80;
return 301 https://$host:8010$request_uri;
}

3. Once edited, please save and close the dynamic.conf.
4. Please go to Windows Services and restart the following MetaDefender MetaDefender Managed File Transfer services for the configuration to be complete:

- OPSWAT MetaDefender Managed File Transfer Helper
- OPSWAT MetaDefender Managed File Transfer Processor
- OPSWAT MetaDefender Managed File Transfer REST

5. The MetaDefender MetaDefender Managed File Transfer web UI should be accessible now.

### [Replace an Expired SSL Certificate](/docs/mdmft/knowledge-base/how-to-troubleshoot-metadefender-managed-file-transfer-becomes-u#replace-an-expired-ssl-certificate)

Before SSL certification replacement, follow the below steps on MFT UI:

1. **Disable HTTPS**: Temporarily turn off HTTPS in MFT to avoid interruptions during the certificate replacement process
2. **Remove Expired SSL Certificat**e: Delete the expired certificate from the MFT configuration to prevent conflicts
3. **Add a Valid SSL Certificate**: Add new, valid SSL certificate
4. **Configure HTTPS**: Configure MFT to use the newly added SSL Certificate
5. **Enable HTTPS Again**: Re-enable HTTPS to secure connections with the newly installed certificate

MFT validates SSL certificates when applying a new SSL certification. If an expired SSL certificate is detected, MFT UI will not respond over HTTPS. In such cases, use the Change Protocol tool to apply a valid SSL certification.

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support-services).

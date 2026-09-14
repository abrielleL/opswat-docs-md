<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/how-do-i-troubleshoot-smtp-and-email-notification-issues-for-met -->

# How do I troubleshoot SMTP and email notification issues for MetaDefender Managed File Transfer?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article applies to all MetaDefender Managed File Transfer (MFT) releases.

When configuring SMTP and email notification functionality, you may encounter some issues if MFT or the environment is configured wrong. Please follow this troubleshooting guide to remediate these issues.

Error

After setting up SMTP and email notification, no emails are sent.

**Cause**: This could be caused by SSL verification issues, invalid recipient, authentication, or other connectivity issues.

**Troubleshooting**: First, open MFT logs to determine if there are any relevant error messages to narrow down the potential causes. Please refer to [How do I find all the MFT logs and their functionality?](https://www.opswat.com/docs/mdmft/knowledge-base/how-do-i-find-all-the-mft-logs-and-its-functionality-) for more info on these logs.

Next, besides MFT logs, you should also verify the following, making sure **all settings are configured properly**:

1. SSL/TLS issue:

   - The correct SMTP port is used, and is open: 25 (unsecure), 465 (SSL/TLS), 587 (STARTTLS).
   - If SSL/TLS is enabled on the SMTP server, it should also be enabled in MFT’s SMTP settings (and vice versa if SSL/TLS is disabled).
   - The SMTP server’s certificate is trusted (i.e. it’s imported to MFT server’s certificate store if it’s self-signed).
   - Check SMTP server’s logs for any relevant error messages.
2. Invalid recipient:

   - No typos in the recipient’s email address, and the recipient exists on the SMTP server.
   - The recipient’s email address is not in the SMTP server’s ban list or blocklist.
   - The recipient’s mail server isn’t down or misconfigured.
3. Authentication errors:

   - The configured username and password on MFT’s SMTP settings are correct.
   - Check the SMTP server logs for errors related to authentication, for example:

     - 535 Authentication unsuccessful – indicates the authentication credentials are incorrect.
     - 530 Must issue a STARTTLS command first – means that SSL/TLS is required for secure authentication.
4. General connectivity errors:

   - You can verify that the SMTP server is reachable from MFT server by performing a simple telnet command to send a test email.
   - If telnet fails, it means the MFT server may not be able to reach the SMTP server, or experiencing other issues related to authentication - use the response code and message to troubleshoot this further.
   - Example: expected telnet responses when everything is working properly.

PowershellCopyPS> Install-WindowsFeature -name Telnet-Client
PS> telnet smtp.server.com 25
220 smtp.server.com ESMTP Postfix
HELO yourdomain.com
250 smtp.server.com
MAIL FROM:<your-email@yourdomain.com>
250 2.1.0 Ok
RCPT TO:<recipient-email@domain.com>
250 2.1.5 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
Subject: Test Email
This is a test email sent from Telnet.
.
250 2.0.0 Ok: queued as 12345
QUIT
221 2.0.0 ByeSuccessful Configuration:

If there is an email sent out after saving SMTP configuration on MetaDefender Managed File Transfer, that should verify a good configuration.

- Notifications can also be triggered to send out a test email to verify emails can be sent.
Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support).

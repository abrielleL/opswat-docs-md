<!-- source: https://www.opswat.com/docs/mdemail/knowledge-base/why-am-i-getting-an--smtp-send-failed-to--response--unable-to-co -->

# Why am I getting an "SMTP send failed to [Response: Unable to connect; Code: 11001]" error?

**Check Your Version:**

This article applies to all Email Gateway Security versions

### [**Issue:**](/docs/mdemail/knowledge-base/why-am-i-getting-an--smtp-send-failed-to--response--unable-to-co#issue)

Some outbound emails failed to send because the Email Gateway Security couldn't connect to the recipient's mail server.

`SMTP send failed to [Response: Unable to connect; Code: 11001]
smtp://domain.mail.protection.outlook.com:25`

This error indicates that the sending server was unable to connect to the recipient's mail server. The most likely causes include:

- DNS resolution failure for the domain [domain.mail.protection.outlook.com](http://domain.mail.protection.outlook.com/)
- Firewall or network restrictions blocking outbound SMTP traffic on port 25
- Temporary service interruption on Microsoft’s mail protection infrastructure (Exchange Online)

The system automatically retried sending the messages, but all attempts failed due to the same connectivity error.

### [**Resolution:**](/docs/mdemail/knowledge-base/why-am-i-getting-an--smtp-send-failed-to--response--unable-to-co#resolution)

Check DNS Resolution, Review Firewall Rules, Check Microsoft Service Status, and Retry Email Delivery.

**Steps:**

1. Test Port 25 Connectivity (Use `telnet` to test if your server can connect to the destination on port 25)

   `telnet domain.mail.protection.outlook.com 25`

   - A successful connection will return something like:

     - *220* [*domain.mail.protection.outlook.com*](http://domain.mail.protection.outlook.com/) *Microsoft ESMTP MAIL Service ready at Wed, 30 Jul 2025 05:35:57 +0000 [08DDCC5163718589]*
   - If it fails to connect or times out, port 25 may be blocked or filtered.
2. **Check DNS Resolution**

   Make sure the domain can be resolved from your sending server:

   `nslookup domain.mail.protection.outlook.com`
3. **Review Firewall Rules**

   Ensure that outbound traffic on TCP port 25 is allowed. Some hosting providers (especially cloud platforms) may block this port by default.
4. **Check Microsoft Service Status**

   Visit [Microsoft 365 Status](https://status.office365.com/) to see if there's a known issue affecting mail delivery.
5. **Retry Email Delivery**

   Once DNS and connectivity issues are resolved, resending the affected messages should succeed.

**Support:**

If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).

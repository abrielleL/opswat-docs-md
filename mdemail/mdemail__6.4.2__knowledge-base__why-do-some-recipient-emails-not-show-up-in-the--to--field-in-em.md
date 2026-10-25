<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/knowledge-base/why-do-some-recipient-emails-not-show-up-in-the--to--field-in-em -->

# Why do some recipient emails not show up in the "To" field in email clients like Outlook although they appear in the EGS processing history?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all versions of MetaDefender Email Gateway Security.

When sending an email to multiple recipients through Email Gateway Security, all recipient addresses appear in the EGS processing history, and the email is successfully delivered to all of them. However, in some email clients like Microsoft Outlook, some of the recipient emails do not show up in the "To" field.

**Explanation:** This behavior occurs because email delivery has two different layers of addressing:

1. **SMTP Envelope (Transport Layer)**

   - Contains the technical delivery information: `MAIL FROM` and `RCPT TO` fields.
   - EGS displays the recipients listed in the **RCPT TO** field. These are the actual recipients that the mail server processes and delivers to.
2. **MIME Headers (Content Layer)**

   - Contains the display information: `To:`, `Cc:`, and `Bcc:` fields.
   - Email clients like Microsoft Outlook and Thunderbird show these fields to end users.
   - These headers are mostly cosmetic and may not always align with the SMTP envelope. For example, if a recipient is included in the SMTP envelope but not in the MIME headers, the email is still delivered, but that recipient will not appear in the Outlook "To" field.

**In Summary:**

- EGS shows the recipients from the SMTP envelope (true delivery list).
- Email clients display the recipients from the MIME headers (cosmetic display list).
- This difference can explain why some recipients are visible in EGS history but not in the Outlook "To" field, even though they still received the email.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

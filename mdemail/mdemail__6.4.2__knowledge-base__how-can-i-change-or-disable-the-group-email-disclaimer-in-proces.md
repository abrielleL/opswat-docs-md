<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/knowledge-base/how-can-i-change-or-disable-the-group-email-disclaimer-in-proces -->

# How Can I Change or Disable the Group Email Disclaimer in Processed Emails?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Context:

After an email has been scanned and sanitized, a blue bar with an information icon appears, displaying the message: "Your email has been processed and modified." You want to change the displayed text or disable this notification.

**Cause**: The blue bar with the message is called the Group Email Disclaimer, which is a default feature ensuring that disclaimers about email processing actions remain short yet informative.

Steps to Disable the Group Email Disclaimer:

1. Log in to the EGS Console.
2. Navigate to Security Rule.
3. Select the rule you want to edit.
4. Go to Advanced Settings.
5. Locate Group Disclaimer Setting.
6. Toggle off Group Disclaimer.
7. Click Save to apply the changes.

Steps to Change the Displayed Text on the Group Disclaimer:

1. Modify the XSLT files used by the product.
2. The default file location is:

- C:\Program Files\OPSWAT\MetaDefender Email Security\mailagenthost\xslt\style_group.xsl

3. Open the file using Notepad or another text editor.
4. Edit the disclaimer text within the file.
5. Save the file and restart the service.
6. View the provided screenshot for further details.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).

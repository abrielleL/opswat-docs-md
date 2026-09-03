<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/knowledge-base/how-do-i-fix-email-content-getting-corrupted-when-using-microsof -->

# How do I fix email content getting corrupted when using Microsoft Exchange mail server?

This article applies to all MetaDefender Email Gateway Security V4 and V5 releases deployed on Windows Systems.

In some cases, when MetaDefender Email Gateway Security is set up with Microsoft Exchange mail server, email contents can get corrupted.

Cause: when the email body is modified (sanitized, redacted, amended with disclaimer, etc.) by MetaDefender Email Gateway Security, the correct encoding is set in the MIME body part headers. Then Exchange also modifies the email but Exchange by default takes the encoding from the <meta> tag of the email body’s HTML code and not from the MIME body part headers. The encoding specification in the MIME body part headers and the <meta> tag may be different, and the MIME body part headers contain the correct encoding. This way Exchange may be mistaken about the encoding. When Exchange applies its modifications to the email, it does not do it with the right encoding and that causes the characters to be corrupted.

Solution:

1. Go to \Program Files\Microsoft\Exchange Server\V15\bin (Note: “V15”, after V can be different number, depending on Exchange version)
2. Create a backup of “EdgeTransport.exe.config“ file
3. Open “EdgeTransport.exe.config“ file in notepad
4. Under the “<appSettings>” tag: add the following line <add key="DisableDetectEncodingFromMetaTag" value="true" />
5. After the config file is saved, restart the Microsoft Exchange Transport service

Support:

In the unlikely event that you have followed the instructions above but are Unable to fix email contents being corrupted when using Microsoft Exchange mail server, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/OPSWATCommunity/s/).

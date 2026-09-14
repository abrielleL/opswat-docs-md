<!-- source: https://www.opswat.com/docs/mdemail/knowledge-base/why-are-hyperlinks-still-active-in-ms-outlook-after-files-have-b -->

# Why are hyperlinks still active in MS Outlook after files have been sanitized by Deep CDR?

This article applies to all MetaDefender Email Gateway Security V4 and V5 releases deployed on Windows Systems.

You may find that, when viewing processed emails in Microsoft Outlook, hyperlinks are active even though Deep CDR was configured to remove them.

Please Note:

This is not an error or indication that the MetaDefender Email Gateway Security system is malfunctioning.

It is a function of the Microsoft Outlook application and, as such, can be disabled.

Outlook has an AutoFormat feature that, among other functions, recognises link text and activates it.

This feature is enabled on Microsoft Outlook by default, but can be disabled via the method detailed [here](https://www.msoutlook.info/question/131).

Once AutoFormat is disabled, Deep CDR’s removal/deactivation of hyperlinks will be retained on emails that are viewed in Microsoft Outlook.

Support:

For further queries, concerns or issues regarding **Seeing Active Hyperlinks On CDR-Processed Emails When They Are Viewed In MS Outlook**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

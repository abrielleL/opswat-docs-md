<!-- source: https://www.opswat.com/docs/mdcloud/knowledge-base/why-is-my-file-is-marked-as-infected-but-no-engine-detected-it- -->

# Why is my file is marked as infected but no engine detected it?

This article applies to all active MetaDefender Cloud license holders - whether your product is paid for or issued for evaluation purposes. For more information on our range of licensing and evaluation options, please [Read This](https://metadefender.opswat.com/licensing).

Occasionally, Multiscan will flag a file as **infected** without reporting which engine detected the threat.

Consider the example in the screenshot below, or click [This Link](https://metadefender.opswat.com/results/file/bzE5MDMwNUh5bGVZa0FCaThFQkpXZUYxQUJpVTQ/regular/overview) to view the example in more detail.

This occurs when the file is an archive (such as the *APK* file in the example above) and one or more of the individual files *inside* the archive have been marked as **infected**.

When scanning the archive as a single file, it may be that no engines detect a threat, but because one or more files inside the archive are **infected**, Multiscan will mark the whole archive as infected.

Support:

For queries or concerns regarding **Positive Threat Results Or MetaDefender Cloud’s Multiscan Functionality**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

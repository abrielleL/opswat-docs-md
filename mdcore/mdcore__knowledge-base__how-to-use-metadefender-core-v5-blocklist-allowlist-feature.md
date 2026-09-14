<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-use-metadefender-core-v5-blocklist-allowlist-feature -->

# How to use MetaDefender Core V5 Blocklist/Allowlist feature?

This article applies to all MetaDefender Core V5 releases deployed on Windows systems.

MetaDefender Core V5.x includes the option to block or allow files by creating a Blocklist or Allowlist. The user can select files to be blocked or allowed based on:

- Filetype group
- MIME-type
- Filename

Full documentation can be found here: [Workflow Configuration Template](/docs/mdcore/configuration/workflow-configuration-template)

The conventional usage of this feature would be, to create a list of files to be blocked or allowed, by any of the three selectors mentioned above (filetype groups, mime-types, file names) or a combination of them.

## [Using filetype groups VS. MIME-types VS file extensions](/docs/mdcore/knowledge-base/how-to-use-metadefender-core-v5-blocklist-allowlist-feature#using-filetype-groups-vs-mime-types-vs-file-extensions)

When possible, It is better to use Filetype groups over MIME types, and MIME types over File names. It is shorter to define, leaves less space for human error and can also leverage OPSWAT's file detection mechanism, so that even if an imposter file has the extension .doc but in reality, it is a .exe it will be treated as .exe

## [Using Regular Expressions](/docs/mdcore/knowledge-base/how-to-use-metadefender-core-v5-blocklist-allowlist-feature#using-regular-expressions)

The rules we create can consist of literal strings but can also include wild cards in the form of Regular Expressions. For example, if we use the string : ^.*.docx$ in the "Blocklist by file names", it will test as True for all files whose name is terminating with docx. Each file processed by MetaDefender Core will be tested against the rules defined in the Blocklist. As soon as any of the rules tests as True the file will be blocked.

## [Advanced usage](/docs/mdcore/knowledge-base/how-to-use-metadefender-core-v5-blocklist-allowlist-feature#advanced-usage)

Sometimes the business rule is something like "Block all files except...". Such a scenario is accommodated in the system by the usage of Regular Expressions. In Regular Expression, we can create an expression that will test as True when a certain string is NOT found (known as Negative Look Ahead) For example, if we use the string: ^.*.((?!docx$).)*$ in the "Blocklist by file names", it will test as True for files whose names do NOT terminate with docx.

- To make the above Regular Expression case insensitive we can use: ^.*.((?![dD][oO][cC][xX]$).)*$

In many cases, we will need to allow more than one file type. For example, if we use the string: ^.*.((?!docx$)(?!xls$).)*$ in the "Blocklist by file names", it will test as True for files whose names do NOT terminate with either docx or xls. The Negative Look Ahead block (?!XYZ$) can be repeated as many times as required.

In the example given above "Block all files except docx" there is a hidden problem. .docx files are actually archive files, containing other files (such as xml, gif, jpeg etc...) This means that if the business rule is **block everything except docx** it most likely means **block everything except docx and all the files it contains.**

Pro Tip:

You can use a tool such as [regex101](https://regex101.com/) to create and test your regular expressions.

Support:

If **Further Assistance** is required then please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).

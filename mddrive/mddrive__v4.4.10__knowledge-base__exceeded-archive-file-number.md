<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/knowledge-base/exceeded-archive-file-number -->

# Status: Exceeded Archive File Number

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Issue](/docs/mddrive/v4.4.10/knowledge-base/exceeded-archive-file-number#issue)

Archive files are skipped during a scan with the status message: ***"Status: Exceeded Archive File Number"***

Skipped scan results with the message: *"Status: Exceeded Archive File Number"*

## [Cause](/docs/mddrive/v4.4.10/knowledge-base/exceeded-archive-file-number#cause)

Some of the archive files being scanned have more child files than the assigned maximum limit.

Archive Handling default values

## [Solution](/docs/mddrive/v4.4.10/knowledge-base/exceeded-archive-file-number#solution)

1. Go to **Settings** ***→*** **Preferences**.
2. Open the **Archive Handling** settings.
3. Increase the **Max number of files extracted** value.

In the following example, the value was changed from the default value of 2000 to 20000:

Change the value of the Max number of files extracted from the Archive Handling Settings

.

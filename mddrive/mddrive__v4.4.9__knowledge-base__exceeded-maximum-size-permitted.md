<!-- source: https://www.opswat.com/docs/mddrive/v4.4.9/knowledge-base/exceeded-maximum-size-permitted -->

# Failed to Request Scan. File size exceeded the maximum size

## [Issue](/docs/mddrive/v4.4.9/knowledge-base/exceeded-maximum-size-permitted#issue)

Files are skipped during a scan with the message: *"Failed to Request Scan. File size exceeded the maximum size permitted for your configuration."*

## [Cause](/docs/mddrive/v4.4.9/knowledge-base/exceeded-maximum-size-permitted#cause)

A scanned file is larger than the **Max File Size** value from the **Scan Settings**. In most cases, the issue occurs because the user doesn't change the **Max File Size** value from the default value, which is 2000.

## [Solution](/docs/mddrive/v4.4.9/knowledge-base/exceeded-maximum-size-permitted#solution)

Increase the **Max File Size to Scan** value:

1. Go to **Settings** → **Preferences** → **Scan**.

The Preferences page

2. In the **Scan Settings** window, set the new **Max File Size** value (in megabytes). In the following image, the value is set to 20,000.

The Scan Settings window

.

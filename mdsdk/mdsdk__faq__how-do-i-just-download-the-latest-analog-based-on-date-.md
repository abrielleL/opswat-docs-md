<!-- source: https://www.opswat.com/docs/mdsdk/faq/how-do-i-just-download-the-latest-analog-based-on-date- -->

# How do I just download the latest analog based on Date?

To download the latest file only if it has been modified since a specific date, use the `If-Modified-Since` command. Cache the previous date, and the server will download the file only if it has been updated since that date.

**Note**: If the specified date is in the future, the file will always be downloaded. The date must fall between the current time and the file's last modified time.

Use the following `curl` command:

BashCopycurl -v -L -O -H "If-Modified-Since: Thu, 17 Jul 2024 16:00:00 GMT"

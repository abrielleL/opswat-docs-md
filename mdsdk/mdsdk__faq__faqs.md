<!-- source: https://www.opswat.com/docs/mdsdk/faq/faqs -->

# How do you handle the license.dat file when going into production?

Many of our partners choose to load the license directly in their code. Here are the possible configurations:

To load the license in your code, you need to use the "License Bytes" during configuration. This requires loading the license.cfg file.

**License Bytes:**

- **Description**: Configuration key for the license byte string. This can be used instead of the license portion of the license.cfg file, corresponding to the value found at `license` in the license.cfg JSON.
- **Note**: If this option is used, automatic license updating is not supported, and WAAPI_CONFIG_LICENSE_KEY_BYTES must be specified.
- **Type**: string
- **Default**: #define WAAPI_CONFIG_LICENSE_BYTES L"license_bytes"

You can also pass the `pass_key` directly in the code. Currently, most sample code reads the file and then passes the string. For more details, refer to [the MDES SDK Documentation](https://software.opswat.com/OESIS_V4/html/c_method.html).

### [How do I just download the latest analog based on Date?](/docs/mdsdk/faq/faqs#how-do-i-just-download-the-latest-analog-based-on-date)

To download the latest file only if it has been modified since a specific date, use the `If-Modified-Since` command. Cache the previous date, and the server will download the file only if it has been updated since that date.

**Note**: If the specified date is in the future, the file will always be downloaded. The date must fall between the current time and the file's last modified time.

Use the following `curl` command:

BashCopycurl -v -L -O -H "If-Modified-Since: Thu, 17 Jul 2024 16:00:00 GMT"

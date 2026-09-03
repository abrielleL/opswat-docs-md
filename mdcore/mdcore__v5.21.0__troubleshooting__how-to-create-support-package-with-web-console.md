<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-with-web-console -->

# How to Create Support Package With Web Console

This article applies to all MetaDefender Core releases **after version 5.13.0**, deployed on both Windows and Linux systems.

Kindly note that the 'Generate Support Package' button is not available in versions earlier than 5.13.0.

Please go to Settings > On the top right click "Generate Support Package"

After that, a sliding windows will open > "Generate"

## [Advance](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-with-web-console#advance)

Info

Users can select which kind of log you want to collect:

- Core: MetaDefender Core's logs
- Nginx: log of nginx
- Engine: log files belong the engines (AV engine, Deep CDR, etc)
- Database: log of PostgreSQL database (if using bundled)
- System: Windows event logs or Linux syslog

The "Limit number of log file" option allows users to choose how many log files the supported package should collect.

Date and Time: Users can select the logs within a specific date and time range.

## [Lightweight](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-with-web-console#lightweight)

Smaller, faster package that captures only the most relevant logs, configuration and recent crash diagnostics needed for initial troubleshooting, minimizing generation time and archive size while still providing enough data for first‑line analysis. With this option, the support package will be generated with predefine options, users don't need to care about the options.

After click `Generate` Please wait for awhile for generating process

After the generating process was done, you can select the support package and download it

You can also find the support package on: Installation folder/data/sp_package.

But we recommend that you should download support package from the UI to avoid break the file.

Support:

If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).

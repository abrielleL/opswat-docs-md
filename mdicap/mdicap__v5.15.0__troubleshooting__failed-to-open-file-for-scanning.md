<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/troubleshooting/failed-to-open-file-for-scanning -->

# Failed to open file for scanning

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This article describes an issue which may occur when stressing (high load) MetaDefender ICAP Server on Windows OS.

## [Symptom](/docs/mdicap/v5.15.0/troubleshooting/failed-to-open-file-for-scanning#symptom)

A lot of requests are blocked with reason "MetaDefender Core is overloaded" or "Failed to open file".

From MetaDefender ICAP Server log:

[WARNING] 2022.05.10 15:55:39.284: (icap.scanner) Failed to open file for scanning, errorDetail='Could not open file C:/Program Files/OPSWAT/Metadefender ICAP Server/data/temp/5bea0e35-6ed1-4c3d-b4e7-e12bcee17783/66fc337d-08bf-4846-89eb-732f1fe66d71 for scanning', connectionId='6a0c7f167f0c4d85ac410cf8f414734e', requestId='364b7516ddc74e31a798c2c3afaf1643' [msgid: 3727]
## [Cause](/docs/mdicap/v5.15.0/troubleshooting/failed-to-open-file-for-scanning#cause)

On Windows OS, the maximum number of files can be opened simultaneously is 512 by default. Anything exceeded will be blocked by Windows OS.

Reference: <https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/setmaxstdio?view=msvc-170>

## [Solution](/docs/mdicap/v5.15.0/troubleshooting/failed-to-open-file-for-scanning#solution)

Use new setting supported on MetaDefender ICAP Server called `maxstdio` to increase the limit (applicable to Windows only). Details: [Configuration file](/docs/mdicap/v5.15.0/configuration/configuration-file)

Since MD ICAP Server v5.2.0, the default value for maxstdio is set to 4096

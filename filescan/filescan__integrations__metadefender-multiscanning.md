<!-- source: https://www.opswat.com/docs/filescan/integrations/metadefender-multiscanning -->

# MetaDefender Multiscanning

The MetaDefender Aether platform can integrate MetaDefender Core API to perform AV engine scans on input/extracted files.

- <https://docs.opswat.com/mdcore/metadefender-core/ref#file-analysis-process>

To enable this integration, please walk through the following steps:

**Step #1 - Copy your MetaDefender Core API key**

If you already have a MetaDefender Core API key, skip to **Step #2.**

Log in to your MetaDefender Core:

- Go to User Management menu
- Find and select your user under Users and Groups tab
- At the API key section, click on Generate and copy your API key

**Step #2 - Update your transform engine configuration in** `/home/sandbox/sandbox/transform.cfg`

transform.cfgCopyenableMetaDefenderAPI=true
metaDefenderUseCloudAPI=false
metaDefenderAPIURL=MY_MDCORE_URL # E.g.: http://10.0.0.5:8008/
metaDefenderAPIKey=MY_API_KEY

For more details, see the [OSINT Lookups](/docs/filescan/configuration/engine-config-osint-lookups) configuration page.

**Step #3 - Scan a file and verify if the OPSWAT MetaDefender Multiscanning results are displayed in the OSINT Lookup section**

It is recommended to test a file that is commonly known, e.g.: a Windows executable.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

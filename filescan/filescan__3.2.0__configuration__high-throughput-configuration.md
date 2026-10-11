<!-- source: https://www.opswat.com/docs/filescan/3.2.0/configuration/high-throughput-configuration -->

# High-Throughput Configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page

To achieve the maximum possible throughput on a single server, make sure to deploy **MetaDefender Sandbox** (previously known as OPSWAT Filescan Sandbox) on a powerful instance:

- 32 vCPUs (preferably 64 vCPUs)
- 128 GB RAM (preferably 256 GB)
- 500 GB SSD (preferably 1 TB)

*The overall throughput of such a server may eclipse the default maximum limit of 25000 scans/day, and it primarily depends on the sample set. The processing time for individual samples can range from 5 seconds to 2 minutes (depending on the complexity of the sample).*

The following special settings can be used to optimize the throughput when the main objective is **quickly obtaining an accurate verdict** for a sample, but deeper analysis is **not required**.

Warning

It is important to set any custom option values in the **transform.cfg** and **broker.cfg** files!

---

## Transform Configuration

Please add the following settings in `/home/sandbox/sandbox/transform.cfg`:

BashCopy# Disable archiving files
archiveTasksAndResourcesIfOlderThanXMinutes=0
deleteArchivedTasksAndResourcesIfOlderThanXMinutes=0
# Delete files older than 60 minutes
deleteTasksAndResourcesIfOlderThanXMinutes=60
deleteResultsPathArtifactsOlderThanXMinutes=60
deleteEmptyDirectoriesIfOlderThanXMinutes=60
deleteTempFilesOlderThanXMinutes=60
# OSINT settings
runOSINTLookups=true
runExtendedOSINTLookups=true
runOSINTLookupsOnExtractedFiles=true
runOSINTLookupsRequireMinProcessingPriority=0
enableOpswatReputationAPI=true
opswatReputationAPIKey=<YOUR MDCLOUD APIKEY>
enableVirusTotalLookups=false
enableClamscanLookup=false
runHexillionOnExtractedDomains=false
runWhoisRecordLookups=false
# Disable expensive/unpredictable subtasks
runFileDownloaders=false
runTesseractOCRForImages=false
runDe4DotForNetFiles=false
runFileVisualizer=false

---

## Webservice Admin Settings

Log in to the sandbox using an admin user, and open the Admin Panel to change the following settings under the Configuration.

#### 1. Configure Reputation Providers (use your `MDCLOUD_API_KEY`):

#### 2. Configure a short retention period for samples and scan reports (e.g. 3 days):

#### 3. Disable Trends-related jobs that might lead to a database bottleneck (**Statistics** tab):

#### 4. Disable other non-essential jobs (**Reports** tab):

#### 5. Configure "Finalize finished reports with hanging subtasks" job to run "Every 2 minutes" (`Scan` tab):

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

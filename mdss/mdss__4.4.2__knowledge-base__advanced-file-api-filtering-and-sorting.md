<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/advanced-file-api-filtering-and-sorting -->

# Advanced File API Filtering and Sorting

**Filtering and sorting** on the File and PDF report APIs include support for a variety of filter and sort combinations.

Some filtering and all sorting parameters support sending a list of values separated by comma, which take part of a logical OR filter (the property can be any of the given values).

## [Filtering](/docs/mdss/4.4.2/knowledge-base/advanced-file-api-filtering-and-sorting#filtering)

Filtering supports the following query parameter fields:

| Query parameter | Possible values | Description | Allows list of values |
| --- | --- | --- | --- |
| **startDate** | A valid DateTime |  | no |
| **endDate** | A valid DateTime |  | no |
| **search** | A string value |  | no |
| **scanType** | - 0 = Instant - 1 = Scheduled - 2 = RealTime |  | yes |
| **storageId** | A valid storage id |  | yes |
| **scanId** | A valid scan id |  | yes |
| **scanWorkflowSnapshotId** | A valid snapshot id |  | yes |
| **processingState** | - InProgress = 0 - Failed = 1 - Canceled = 2 - Available = 3 | State of processing in MDSS | yes |
| **result** | - 0 = Allowed - 1 = Blocked - 2 = Processing | Result of MDSS | yes |
| **scanAllResultI** | - See [core result codes](https://www.opswat.com/docs/mdcore/integration/description-of-scan-result-codes) | General result of the Scan Instance | yes |
| **scanResultICount** | An integer >= 0 | The number of engine results that are not "No threat detected" | yes |
| **vulnerabilityCount** | An integer >= 0 | The number of vulnerabilities detected | yes |
| **dlpDetection** | Boolean true or false | DLP detection | no |
| **remediations** | - 0 = Tagging - 1 = DeepCdrSanitization - 2 = DeepCdrDelete - 3 = DeepCdrEncrypt - 4 = DeepCdrKeep - 5 = AllowedMoved - 6 = BlockedMoved - 7 = BlockedDelete - 8 = SanitizedMoved - 9 = AllowedCopied - 10 = BlockedCopied - 11 = SanitizedCopied - 100 = SoftDelete | Remediations performed | yes |

## [Sorting](/docs/mdss/4.4.2/knowledge-base/advanced-file-api-filtering-and-sorting#sorting)

Sorting supports multiple parameters, which are used if there is an equality between the values of the preceding sort. If multiple sorts are used, the property and order are matched in order between the two lists of values. The following query parameter fields are available:

| Query parameter | Possible values |
| --- | --- |
| **sortBy** | - 0 = DiscoveryStarted - 1 = ScanId - 2 = ProcessingState - 3 = Result - 4 = ScanAllResultI - 5 = ScanResultICount |
| **sortOrder** | - 0 = Ascending - 1 = Descending |

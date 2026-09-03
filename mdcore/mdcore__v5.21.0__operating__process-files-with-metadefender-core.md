<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/operating/process-files-with-metadefender-core -->

# Process files with MetaDefender Core

There are several ways to scan files with MetaDefender Core:

## [Process Files via REST API](/docs/mdcore/v5.21.0/operating/process-files-with-metadefender-core#process-files-via-rest-api)

The MetaDefender Core server also provides a REST API to interface with the application. To process a file even the user interface uses this API.

Raw binary file content must be packed in a single payload and streamed over to MetaDefender Core.

Chunked transfer encoding is not supported to upload files for processing.

All the responses from the server are in JSON format for easy parsing.

### [How to Interact with MetaDefender Core using REST](/docs/mdcore/v5.21.0/operating/process-files-with-metadefender-core#how-to-interact-with-metadefender-core-using-rest)

Beginning with MetaDefender Core 4.x, OPSWAT recommends using the JSON-based REST API. The available methods are documented ([Full REST API documentation](/docs/mdcore/v5.21.0/metadefender-core)).

### [File analysis process](/docs/mdcore/v5.21.0/operating/process-files-with-metadefender-core#file-analysis-process)

1. Upload a file to scan (`POST /file`), then receive data_id from response: ([Scan File](/docs/mdcore/v5.21.0/metadefender-core#fileanalysispost)). Note: The performance depends on:

   - number of engines
   - type of file to be scanned
   - MetaDefender Core's hardware
2. Fetch the result with previously received data_id (`GET /file/{data_id}`) until scan result belonging to data_id doesn't reach the 100 percent progress_percentage: ([GET Fetch Analysis Result](/docs/mdcore/v5.21.0/metadefender-core#fileanalysisget)). Note: Too many data_id requests can reduce performance. It is enough to just check every few hundred milliseconds.
3. Retrieve the scan results anytime after the scan is completed with hash for files (md5, sha1, sha256). (The hash can be found in the scan results) ([GET Fetch Analysis Result](/docs/mdcore/v5.21.0/metadefender-core#fileanalysisget))

## [Analyze Files via Web Interface](/docs/mdcore/v5.21.0/operating/process-files-with-metadefender-core#analyze-files-via-web-interface)

Once you open your browser and go to the MetaDefender Core server's URL the public file processing interface will be displayed.

### [Choose what to process and how](/docs/mdcore/v5.21.0/operating/process-files-with-metadefender-core#choose-what-to-process-and-how)

There are two option fields in the middle of the page. Next to them there is the **PROCESS FILE** button. With the leftmost option you can select between the available workflows for the public file processing. These workflows are determined by the MetaDefender Core administrators, so it is possible that only one workflow will be available for public scanning, or even none.

The next option is where you choose the file to scan. Click on the **SELECT A FILE** button and browse to the file to be scanned.

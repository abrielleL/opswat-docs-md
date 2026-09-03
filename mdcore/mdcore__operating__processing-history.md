<!-- source: https://www.opswat.com/docs/mdcore/operating/processing-history -->

# Processing history

The Scan History page shows information on all scans made on the MetaDefender Core. Search and filter are also supported against each scan result attribute.

If an archive was scanned, its details popup will include tabs for the original files scan details and also a list with the results of the contained files.

On the Processing history page you can also search for:

- MD5, SHA1, SHA256, SHA512 hashes.
- File name (and you can limit search result for a specific scan result, and for specific username who submitted files)
- Source (IP address)
- User name

There is an option to export scan history in CSV or STIX format. For the export, the Result filter can also be applied.

- The user can export STIX file by clicking on STIX export button. In addition to set Result filter, STIX file will contain only blocked scans. After the desired time range selected, the download will be started by clicking on the OK button.
- CSV file is accessible by clicking on the CSV export button, and pressing OK after the desired time range selected.

## [Cleanup processing history](/docs/mdcore/operating/processing-history#cleanup-processing-history)

The processing history data will be automatically cleaned up based on the configured settings under **Settings > Data Retention**. Additionally, users can manually clean up the processing history by navigating to **History > Processing** and selecting the **Cleanup** button.

Warning

When the **"Clean All"** option is selected, please be aware that all data will be permanently removed.

This action can only be performed when no files are being scanned.

This action may take some time to complete. During this period, please refrain from adding any files for processing.

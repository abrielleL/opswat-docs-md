<!-- source: https://www.opswat.com/docs/my/support-services/how-to-identify-actionable-files -->

# Important Upload File Limitation

The submission form supports only a single file upload (maximum size: 2 GB). If multiple files need to be submitted, they must be compressed into a ZIP archive.

Requests that contain more than **3 actionable files** will be rejected. An *actionable file* is any individual file within the archive that requires analysis as part of the false detection request.

To help identify actionable items:

- **False positives**: In MetaDefender Core, enable the **Blocked leaf** option. This view shows only the files that require action in a false positive case.![](https://uploads.developerhub.io/prod/JYvy/ejz34yhodre2o1mcsfypewm2d6k2ahg63ir88c0gynmql467snc9jdq7yzv5sumf.png)

![](https://uploads.developerhub.io/prod/JYvy/nh2u4mn7054rcalpksravpjvogbrr0iwsjrl8ez5g9096bj3xloohwxztv3vtto3.png)

- **False negatives**: Users may choose which files to include.

Users may attach additional files for context without limitation — only actionable files count toward the three-file limit.

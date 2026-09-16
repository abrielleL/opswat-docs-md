<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-do-i-remediate-metadefender-core-using-too-much-resource-whi -->

# How do I remediate MetaDefender Core using too much resource while sanitizing TIFF/TIF image file?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

### [**Issue**](/docs/mdcore/v5.22.0/knowledge-base/how-do-i-remediate-metadefender-core-using-too-much-resource-whi#issue)

When processing TIFF/TIF image files, you may notice some behaviors such as:

- Deep CDR sanitization of the TIFF/TIF image takes a long time.
- High resource usage (CPU, memory, disk space).
- Other scan requests getting timed out while waiting in queue.

### [**Cause**](/docs/mdcore/v5.22.0/knowledge-base/how-do-i-remediate-metadefender-core-using-too-much-resource-whi#cause)

TIFF/TIF image files can have many pages (multi-page TIFF files). When the Deep CDR engine processes them, it needs to extract and handle each page. While the original size of the image may be small, the size of the decompressed image can be quite big, which contributes to the increased resource usage and sanitization time.

For example:

- A TIFF file with size of 2.35 MB, containing 30 pages.
- Each page’s dimension is 2496 x 3507, meaning that the total decompressed (raw) size could be about 250 MB.

### [**Remediation**](/docs/mdcore/v5.22.0/knowledge-base/how-do-i-remediate-metadefender-core-using-too-much-resource-whi#remediation)

You can set some limitations to TIFF/TIF image processing, to avoid using up all the system's resources and slowing down other processing requests.

In Workflow > Deep CDR > File type handling > Image:

- **TIFF Size Limit (MB):** This limits the raw decompressed size of TIFF image that Deep CDR can handle ([Deep CDR Image Limit Configurations](/docs/mdcore/v5.22.0/deep-cdr/image-limit-configurations)).
- **Restrict processing of big TIFF files in single thread:** Any TIFF file with a decompressed image size greater than or equal to 128MB will be processed in single-thread mode. Files with a decompressed image size of 128MB or less will continue to be processed in multi-thread mode.
- **Deep Sanitization:** By turning this off, CDR will only validate file structure and check for any tailing data after the end of the file and remove that part. This is faster, but the tradeoff is less secure compared to the having this option on, which is the default.

If enough system memory is available, you can increase the **Image Memory Limit (MB)** in Deep CDR's engine settings to get more of the processing done on memory rather than on disk.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).

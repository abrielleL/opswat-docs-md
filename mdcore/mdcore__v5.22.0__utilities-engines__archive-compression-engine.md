<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/utilities-engines/archive-compression-engine -->

# Archive Compression Engine

Archive Compression is commonly used in conjunction with the Deep CDR engine for sanitizing archive files. While the Deep CDR engine sanitizes the files within an archive, the Archive Compression engine compresses the sanitized files back into a new archive. For more detailed information, please refer to this page: [Archive Sanitization](/docs/mdcore/v5.22.0/deep-cdr/archive-sanitization).

Additionally, if you are using DLP without Deep CDR, you can configure Archive Compression to work with DLP. In this case, the compressed output file will contain both allowed files and files processed by Proactive DLP.

Archive Compression also includes the capability to retain the original password of the archive.

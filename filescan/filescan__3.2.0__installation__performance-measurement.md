<!-- source: https://www.opswat.com/docs/filescan/3.2.0/installation/performance-measurement -->

# Performance Measurement Per Filetype

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Description

Performance management in this context refers to the assessment of the system’s ability to handle various file types efficiently. The goal is to measure throughput across different configurations, ensuring optimal resource allocation and system stability. By analyzing scan rates, processing efficiency, and system bottlenecks, performance management helps in identifying improvements and maintaining consistent performance under different workloads.

### [Test Configurations](/docs/filescan/3.2.0/installation/performance-measurement#test-configurations)

| **Setup** | **CPU Cores** | **Ram** | **Parallel Count** |
| --- | --- | --- | --- |
| Config 1 | 8 | 16 GB | 5 |
| Config 2 | 16 | 32 GB | 10 |
| Config 3 | 20 | 32 GB | 15 |

Warning

For optimal performance, ensure that the number of CPU cores allocated is at least equal to the configured parallel count. This helps prevent resource bottlenecks and maximizes processing efficiency.

## [Data Set](/docs/filescan/3.2.0/installation/performance-measurement#data-set)

| File Category | File Type | Number of files | Total Size (MB) | Average Size (MB) |
| --- | --- | --- | --- | --- |
| Adobe | PDF | 75 | 81 | 0.93 |
| Executable | EXE | 6 | 65 | 0.09 |
|  | MSI | 3 | 9,6 | 0.31 |
| Image | BMP | 16 | 108.6 | 0.15 |
|  | JPG | 84 | 49.8 | 1.69 |
|  | PNG | 69 | 35.4 | 1.9 |
| Media | MP3 | 27 | 181.1 | 0.15 |
|  | MP4 | 10 | 105.9 | 0.09 |
| Office | DOC | 45 | 102 | 0.44 |
|  | DOCX | 47 | 40 | 1.17 |
|  | ODS | 22 | 6.2 | 3.55 |
|  | ODT | 18 | 1 | 18 |
|  | PPT | 71 | 409.8 | 0.17 |
|  | PPTX | 73 | 181.3 | 0.40 |
|  | XLS | 67 | 59.7 | 1.12 |
|  | XLSX | 68 | 59.6 | 1.14 |
| Text | CHM | 11 | 1.9 | 5.79 |
|  | CSV | 20 | 49.5 | 0.40 |
|  | EML | 6 | 13 | 0.46 |
|  | HTML | 215 | 16 | 13.44 |
|  | RTF | 19 | 6.4 | 2.99 |
|  | TXT | 100 | 44.1 | 2.27 |

## [Throughput Results](/docs/filescan/3.2.0/installation/performance-measurement#throughput-results)

Adobe, Executable, Office, Text, Image, Media

### [Scans Per Day](/docs/filescan/3.2.0/installation/performance-measurement#scans-per-day)

| **File Type** | Config **1** | Config **2** | Config **3** |
| --- | --- | --- | --- |
| Adobe | 9,552 | 17,280 | 23,784 |
| Executable | 22,296 | 35,472 | 46,516 |
| Office | 9,312 | 14,400 | 18,768 |
| Text | 13,392 | 15,384 | 17,832 |
| Image | 42,336 | 96,240 | 123,120 |
| Media | 37,728 | 74,736 | 111,072 |

### [Average processing time per file](/docs/filescan/3.2.0/installation/performance-measurement#average-processing-time-per-file)

Info

The average processing times shown are approximations, assuming that file types with dynamic analysis support often included dynamic analysis in their processing. This may slightly influence the observed times, especially for complex file types like executables and office documents.

Processing times in MetaDefender Core may vary slightly from these values, and real-world processing times can differ depending on the specific file type mix encountered in different environments.

| **File Type** | Config **1** | Config **2** | Config **3** |
| --- | --- | --- | --- |
| Adobe | 18.0 sec | 8.1 sec | 6.6 sec |
| Executable | 12.9 sec | 8.9 sec | 4.8 sec |
| Office | 18.0 sec | 12.2 sec | 8.5 sec |
| Text | 12.5 sec | 8.7 sec | 8.4 sec |
| Image | 4.2 sec | 2.9 sec | 2.7 sec |
| Media | 4.6 sec | 4.2 sec | 2.8 sec |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

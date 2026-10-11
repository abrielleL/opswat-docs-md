<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/installation/performance-measurement -->

# Performance measurement

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [1. Product Information](/docs/mdkiosk/v4.8.6/installation/performance-measurement#1-product-information)

Product versions to be tested:

- MetaDefender Kiosk 4.8.4.8500
- MetaDefender Managed File Transfer 3.9.3.0
- MetaDefender Core 5.20.0
- KIOSK Hardened Image version: 26.07.0
- Engines:

  - Metascan:

    - 22 AV engines package + Crowdstrike when testing with CAB file
    - MAX AV engines package when testing with mixed dataset
    - 9 AV engines package when testing with mixed dataset
  - Deep CDR: 7.6.3
  - Proactive DLP: 3.1.0
  - Archive: 7.6.2
  - FileType: 7.6.2
  - File-Based Vulnerability Assessment: 4.2.416.0

## [2. Environment](/docs/mdkiosk/v4.8.6/installation/performance-measurement#2-environment)

#### [MetaDefender Kiosk devices](/docs/mdkiosk/v4.8.6/installation/performance-measurement#metadefender-kiosk-devices)

Using the KIOSK devices in the local test environment. MetaDefender Core is installed on the same system as MetaDefender Kiosk.

| **Model** | **CPU** | **Memory (GB)** | **Disk type** | **OS** |
| --- | --- | --- | --- | --- |
| Kiosk Desktop (Dell 7420) | Intel Core i9-14900  Cores: 24  Logical processors: 24 Base speed: 2.00 GHz | 32 | SSD | Windows 10 IoT Enterprise LTSC  Version: 21H2 |
| Kiosk Desktop (Dell Pro 24) | Intel Core Ultra 9 285  Cores: 24  Logical processors: 24 Base speed: 2.50 GHz | 32 | SSD | Windows 10 IoT Enterprise LTSC  Version: 21H2 |
| Kiosk Mobile (Dell Pro Rugged 12) | Intel Core Ultra 7 268V  Cores: 8  Logical processors: 8 Base speed: 2.20 GHz | 32 | SSD | Windows 10 IoT Enterprise LTSC  Version: 21H2 |
| Kiosk Tower (Dell D19U) | Intel Core Ultra 9 285  Cores: 24  Logical processors: 24 Base speed: 2.50 GHz | 32 | SSD | Windows 10 IoT Enterprise LTSC  Version: 21H2 |

#### [Storage Device](/docs/mdkiosk/v4.8.6/installation/performance-measurement#storage-device)

Using to store the dataset and connect to the Kiosk device: 128GB SanDisk USB 3.2 Gen 1

#### [MFT Server](/docs/mdkiosk/v4.8.6/installation/performance-measurement#mft-server)

In case the MD Kiosk sends files to MD MFT after scanning, MD MFT is a virtual machine with the following specifications:

| **OS** | **vCPU** | **Memory (GB)** | **Disk type** | **Network bandwidth (Gbps)** |
| --- | --- | --- | --- | --- |
| Windows Server 2022 | 8 | 16 | SSD | 10 Gb Ethernet |

#### [Client](/docs/mdkiosk/v4.8.6/installation/performance-measurement#client)

Using to run the Python script. The Client is a virtual machine with the following specifications:

| **OS** | **vCPU** | **Memory (GB)** | **Disk type** | **Network bandwidth (Gbps)** |
| --- | --- | --- | --- | --- |
| CentOS Linux 7.9 | 8 | 16 | SSD | 10 Gb Ethernet |

## [3. Test flows](/docs/mdkiosk/v4.8.6/installation/performance-measurement#3-test-flows)

- Flow 1: MD Kiosk sends Mixed dataset to MD Core (MAX AV engines + CDR + DLP + Vul) for scanning.
- Flow 2: MD Kiosk sends Mixed dataset to MD Core (9 AV engines + CDR + DLP + Vul) for scanning.
- Flow 3: MD Kiosk sends CAB file to MD Core (22 AV engines + CDR + DLP + Vul) for scanning.
- Flow 4: MD Kiosk sends Mixed dataset to MD Core (9 AV engines) for scanning, and Allowed files are copied to MD MFT as a zip.
- Flow 5: MD Kiosk sends Mixed dataset to MD Core (9 AV engines) for scanning, and Allowed files are copied to MD MFT in a folder.
- Flow 6: MD Kiosk sends Mixed dataset to MD Core (9 AV engines) for scanning, and Allowed files are copied to a shared network folder.
- Flow 7: MD Kiosk self-scans its internal storage (9 AV engines).

## [4. Dataset](/docs/mdkiosk/v4.8.6/installation/performance-measurement#4-dataset)

**CAB file:**

- Extracted files: 849,479
- Total size of extracted files: 26.5 GB

**Mixed dataset:**

- Summary (compressed):

  - Number of files: 5000
  - Total size: 7728.5 MB
  - Average file size: 1.55 MB
- Summary (extracted):

  - Number of files: 5260
  - Total size: 7759.5 MB
  - Average file size: 1.48 MB
- Largest file size: 24.7 MB
- Smallest file size: 5 KB

| **File category** | **File type** | **Number of files** | **Total size (MB)** | **Average file size (MB)** |
| --- | --- | --- | --- | --- |
| Adobe | PDF | 370 | 385 MB | 1.0 MB |
| Executable | EXE | 45 | 309.5 MB | 6.9 MB |
|  | MSI | 15 | 45.75 MB | 3.1 MB |
| Image | BMP | 80 | 515 MB | 6.4 MB |
|  | JPG | 420 | 237.5 MB | 0.6 MB |
|  | PNG | 345 | 169 MB | 0.5 MB |
| Media | MP3 | 135 | 865 MB | 6.4 MB |
|  | MP4 | 50 | 500 MB | 10.0 MB |
| Office | DOCX | 235 | 190 MB | 0.8 MB |
|  | DOC | 225 | 486 MB | 2.2 MB |
|  | PPTX | 365 | 860 MB | 2.4 MB |
|  | PPT | 355 | 1950 MB | 5.5 MB |
|  | XLSX | 340 | 283.5 MB | 0.8 MB |
|  | XLS | 335 | 284.5 MB | 0.8 MB |
| Text | CSV | 100 | 236 MB | 2.4 MB |
|  | HTML | 1075 | 76 MB | 0.1 MB |
|  | TXT | 500 | 210 MB | 0.4 MB |
| Archive | ZIP | Compressed files: 10  Extracted files: 270 | Compressed size: 125.5 MB  Extracted size: 156.5 MB | Avg compressed size: 12.6 MB  Avg extracted size: 0.6 MB |

## [5. MetaDefender Core settings](/docs/mdkiosk/v4.8.6/installation/performance-measurement#5-metadefender-core-settings)

General settings

- Turn off data retention
- Turn off the engine update
- Max size:

  - File scan: 9999999999999 MB
  - URL file download: 9999999999999 MB

Metascan

- Enable engines depend on the testing package
- Per AV engine scan: 1 min
- Global scan: 10 mins
- File download: 5 mins

Deep CDR

- Enable engine
- 135 file types

Proactive DLP

- Enable engine

Archive Extraction

- Enable engine
- Max recursive level: 99999999
- Max number of files extracted: 99999999
- Max total size of extracted files: 99999999
- Timeout: 90 mins

Archive Compression

- Enable engine

FileType

- Enable engine
- Timeout: 5 mins

File-Based Vulnerability Assessment

- Enable engine

## [6. Test Summary](/docs/mdkiosk/v4.8.6/installation/performance-measurement#6-test-summary)

#### [Flow 1: MD Kiosk sends Mixed dataset to MD Core (MAX AV engines + CDR + DLP + Vul) for scanning.](/docs/mdkiosk/v4.8.6/installation/performance-measurement#flow-1-md-kiosk-sends-mixed-dataset-to-md-core-max-av-engines--cdr--dlp--vul-for-scanning)

| Device | Duration | Avg. CPU Usage | Avg. Memory Usage | Avg. Disk Speed (KB/s) | Throughput (objects/hour) | Throughput (files/hour) |
| --- | --- | --- | --- | --- | --- | --- |
| **Kiosk Desktop (Dell Pro 24)** | 1 hour 48 minutes | 40.5% | 77.4% | Read 6,018.1 Write 8,240.6 | 72,262.8 | 2,776.1 |
| **Kiosk Desktop (Dell 7420)** | 2 hours 5 minutes | 65.2% | 80.7% | Read 7,355.3 Write 8,265.4 | 62,487.6 | 2,400.0 |
| **Kiosk Mobile (Dell Pro Rugged 12)** | 2 hours 44 minutes | 77.9% | 74.2% | Read 4,185.7 Write 5,507.3 | 47,571.4 | 1,827.4 |
| **Kiosk Tower (Dell D19U)** | 1 hour 43 minutes | 44.1% | 79.3% | Read 6,515.8 Write 10,386.7 | 75,989.0 | 2,918.8 |

#### [Flow 2: MD Kiosk sends Mixed dataset to MD Core (9 AV engines + CDR + DLP + Vul) for scanning.](/docs/mdkiosk/v4.8.6/installation/performance-measurement#flow-2-md-kiosk-sends-mixed-dataset-to-md-core-9-av-engines--cdr--dlp--vul-for-scanning)

| Device | Duration | Avg. CPU Usage | Avg. Memory Usage | Avg. Disk Speed (KB/s) | Throughput (objects/hour) | Throughput (files/hour) |
| --- | --- | --- | --- | --- | --- | --- |
| **Kiosk Desktop (Dell Pro 24)** | 56 minutes | 20.7% | 49.3% | Read 6,610.7 Write 10,097.5 | 140,626.4 | 5,389.2 |
| **Kiosk Desktop (Dell 7420)** | 54 minutes | 49.3% | 49.1% | Read 7,455.6 Write 11,723.5 | 145,528.0 | 5,588.3 |
| **Kiosk Mobile (Dell Pro Rugged 12)** | 1 hour 17 minutes | 49.4% | 40.6% | Read 4,600.8 Write 7,152.6 | 101,189.1 | 3,886.8 |
| **Kiosk Tower (Dell D19U)** | 41 minutes | 26.0% | 47.4% | Read 9,724.9 Write 13,789.3 | 190,923.4 | 7,332.0 |

#### [Flow 3: MD Kiosk sends CAB file to MD Core (22 AV engines + CDR + DLP + Vul) for scanning.](/docs/mdkiosk/v4.8.6/installation/performance-measurement#flow-3-md-kiosk-sends-cab-file-to-md-core-22-av-engines--cdr--dlp--vul-for-scanning)

| Device | Duration | Avg. CPU Usage | Avg. Memory Usage | Avg. Disk Speed (KB/s) | Throughput (objects/hour) | Throughput (files/hour) |
| --- | --- | --- | --- | --- | --- | --- |
| **Kiosk Desktop (Dell Pro 24)** | 2 hours 13 minutes | 71.8% | 67.4% | Read 6,193.9 Write 27,506.7 | 557,797.6 | 0.5 |
| **Kiosk Desktop (Dell 7420)** | 4 hours 7 minutes | 54.6% | 66.0% | Read 3,226.1 Write 15,117.3 | 206,260.3 | 0.2 |
| **Kiosk Mobile (Dell Pro Rugged 12)** | 6 hours 1 minute | 95.4% | 69.9% | Read 1,154.3 Write 9,809.4 | 141,167.5 | 0.2 |
| **Kiosk Tower (Dell D19U)** | 2 hours 5 minutes | 69.3% | 71.2% | Read 5,624.7 Write 27,025.3 | 408,155.5 | 0.5 |

#### [Flow 4: MD Kiosk sends Mixed dataset to MD Core (9 AV engines) for scanning, and Allowed files are copied to MD MFT as a zip.](/docs/mdkiosk/v4.8.6/installation/performance-measurement#flow-4-md-kiosk-sends-mixed-dataset-to-md-core-9-av-engines-for-scanning-and-allowed-files-are-copied-to-md-mft-as-a-zip)

| Device | Duration | Avg. CPU Usage | Avg. Memory Usage | Avg. Disk Speed (KB/s) | Avg. Network Speed (KB/s) | Throughput (objects/hour) | Throughput (files/hour) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Kiosk Mobile (Dell Pro Rugged 12)** | 1 hour 20 minutes | 18.3% | 33.4% | Read 5,418.0 Write 8,096.9 | Receive 2,655.4 Send 2,039.8 | 253,993.1 | 3,755.5 |

#### [Flow 5: MD Kiosk sends Mixed dataset to MD Core (9 AV engines) for scanning, and Allowed files are copied to MD MFT in a folder.](/docs/mdkiosk/v4.8.6/installation/performance-measurement#flow-5-md-kiosk-sends-mixed-dataset-to-md-core-9-av-engines-for-scanning-and-allowed-files-are-copied-to-md-mft-in-a-folder)

| Device | Duration | Avg. CPU Usage | Avg. Memory Usage | Avg. Disk Speed (KB/s) | Avg. Network Speed (KB/s) | Throughput (objects/hour) | Throughput (files/hour) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Kiosk Desktop (Dell Pro 24)** | 1 hour 24 minutes | 6.6% | 33.5% | Read 5,371.0 Write 7,901.6 | Receive 639.4 Send 1,658.0 | 137,058.4 | 3,586.4 |

#### [Flow 6: MD Kiosk sends Mixed dataset to MD Core (9 AV engines) for scanning, and Allowed files are copied to a shared network folder.](/docs/mdkiosk/v4.8.6/installation/performance-measurement#flow-6-md-kiosk-sends-mixed-dataset-to-md-core-9-av-engines-for-scanning-and-allowed-files-are-copied-to-a-shared-network-folder)

| Device | Duration | Avg. CPU Usage | Avg. Memory Usage | Avg. Disk Speed (KB/s) | Avg. Network Speed (KB/s) | Throughput (objects/hour) | Throughput (files/hour) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Kiosk Tower (Dell D19U)** | 59 minutes | 8.8% | 33.2% | Read 6,270.8 Write 7,723.6 | Receive 1,376.0 Send 2,310.3 | 180,628.2 | 5,093.4 |

#### [Flow 7: MD Kiosk self-scans its internal storage (9 AV engines).](/docs/mdkiosk/v4.8.6/installation/performance-measurement#flow-7-md-kiosk-self-scans-its-internal-storage-9-av-engines)

| Device | Duration | Avg. CPU Usage | Avg. Memory Usage | Avg. Disk Speed (KB/s) | Throughput (objects/hour) | Throughput (files/hour) |
| --- | --- | --- | --- | --- | --- | --- |
| **Kiosk Desktop (Dell Pro 24)** | 1 hour 28 minutes | 77.1% | 42.0% | Read 16,971.6 Write 36,570.8 | 616,693.0 | 200,245.8 |

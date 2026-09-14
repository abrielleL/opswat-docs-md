<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/installation/performance-of-post-processed-files-copying-to-directory -->

# Copying to Directory

## [1. Environment](/docs/mdkiosk/v4.8.5/installation/performance-of-post-processed-files-copying-to-directory#1-environment)

Using the K1001 model device in the local test environment. This is a controlled, isolated environment.

| Server | vCPU | Memory (GB) | OS | Disk type |
| --- | --- | --- | --- | --- |
| MD KIOSK (K1001) | 24 | 32 | Windows 10 IoT Enterprise | SSD |

### [**Storage Device (stores data & connects to MD KIOSK server)**](/docs/mdkiosk/v4.8.5/installation/performance-of-post-processed-files-copying-to-directory#storage-device-stores-data--connects-to-md-kiosk-server)

2TB HDD LaCie Rugged Thunderbolt USB-C

### [**Network Bandwidth**](/docs/mdkiosk/v4.8.5/installation/performance-of-post-processed-files-copying-to-directory#network-bandwidth)

1 Gigabit Ethernet

## [2. Test flow](/docs/mdkiosk/v4.8.5/installation/performance-of-post-processed-files-copying-to-directory#2-test-flow)

Files are scanned by MD Core and Allowed files are uploaded to Directory.

## [3. Dataset](/docs/mdkiosk/v4.8.5/installation/performance-of-post-processed-files-copying-to-directory#3-dataset)

Dataset of 900,000 files totaling ~1TB

## [4. Product versions to be tested](/docs/mdkiosk/v4.8.5/installation/performance-of-post-processed-files-copying-to-directory#4-product-versions-to-be-tested)

- MD Kiosk 4.6.6
- MD Core 5.8.0

  - Anti-virus: 1 engine ESET
  - DLP: off
  - CDR: off
  - Vulnerability: off
  - Archive: off
  - FileType: 6.5.1

## [5. Test result](/docs/mdkiosk/v4.8.5/installation/performance-of-post-processed-files-copying-to-directory#5-test-result)

Scan time: 11h 56m 17s

| **File Explorer** | **1 thread** | **50 threads** |
| --- | --- | --- |
| more than **6 hours** | - Copy time: **7h 3m 39s** - Throughput (files/hour): 127,463.7 | - Copy time: **4h 16m 2s** - Throughput (files/hour): 210,910 |

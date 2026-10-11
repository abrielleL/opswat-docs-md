<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/installation/performance-of-post-processed-files-copying-to-usb -->

# Copying to User Media

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [1. Environment](/docs/mdkiosk/v4.8.6/installation/performance-of-post-processed-files-copying-to-usb#1-environment)

Using the K1001 model device in the local test environment. This is a controlled, isolated environment.

| Server | vCPU | Memory (GB) | OS | Disk type |
| --- | --- | --- | --- | --- |
| MD KIOSK (K1001) | 24 | 32 | Windows 10 IoT Enterprise | SSD |

### [**Source media**](/docs/mdkiosk/v4.8.6/installation/performance-of-post-processed-files-copying-to-usb#source-media)

64GB Sandisk Cruzer Glide USB 3.0

### [**Destination media**](/docs/mdkiosk/v4.8.6/installation/performance-of-post-processed-files-copying-to-usb#destination-media)

64GB Kanguru FlashTrust USB 3.0

## [2. Test flow](/docs/mdkiosk/v4.8.6/installation/performance-of-post-processed-files-copying-to-usb#2-test-flow)

Files are scanned by MD Core and Allowed files are uploaded to User Media.

## [3. Dataset](/docs/mdkiosk/v4.8.6/installation/performance-of-post-processed-files-copying-to-usb#3-dataset)

Dataset of 15,000 files totaling +37GB

## [4. Product versions to be tested](/docs/mdkiosk/v4.8.6/installation/performance-of-post-processed-files-copying-to-usb#4-product-versions-to-be-tested)

- MD Kiosk 4.6.6
- MD Core 5.8.0

  - Anti-virus: 1 engine ESET
  - DLP: off
  - CDR: off
  - Vulnerability: off
  - Archive: off
  - FileType: 6.5.1

## [5. Test result](/docs/mdkiosk/v4.8.6/installation/performance-of-post-processed-files-copying-to-usb#5-test-result)

Scan time: 1h 2m 26s

| **1 thread** | **50 threads** | **100 threads** |
| --- | --- | --- |
| - Copy time: **28m 47s** - Throughput (files/hour): 31,250 | - Copy time: **28m 26s** - Throughput (files/hour): 31,914.9 | - Copy time: **29m 22s** - Throughput (files/hour): 30,612.2 |

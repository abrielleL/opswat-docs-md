<!-- source: https://www.opswat.com/docs/filescan/3.2.0/configuration/engine-config-basic-features -->

# Basic Features

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Step #1 - Open** `/home/sandbox/sandbox/transform.cfg` **in a text editor**

**Step #3 - Save the file and restart the** `sandbox` **service**

## [Second Stage Malware Detection](/docs/filescan/3.2.0/configuration/engine-config-basic-features#second-stage-malware-detection)

Enable file downloads to detect 2nd stage malware downloaded from the Internet

transform.cfgCopyrunFileDownloaders=true
runFileDownloaderTimeoutMs=60000
fileDownloaderMaxFileDownloads=10

| Property name | Default value | Description |
| --- | --- | --- |
| runFileDownloaders | true | Main switch to enable file downloads |
| runFileDownloaderTimeoutMs | 1 minute | Execution timeout |
| fileDownloaderMaxFileDownloads | 10 | Download limit, '0' means no limit. |

## [Malware Config Extraction](/docs/filescan/3.2.0/configuration/engine-config-basic-features#malware-config-extraction)

Enable [malware config extraction](https://docs.opswat.com/filescan/datasheet/supported-malwares-for-config-extraction)

transform.cfgCopymalwareConfigExtractionEnabled=true
malwareConfigExtractionMaxInputFileSize=100

| Property name | Default value | Description |
| --- | --- | --- |
| malwareConfigExtractionEnabled | true | Switch to enable / disable malware config extraction |
| malwareConfigExtractionMaxInputFileSize | 100 MB | File size limit |

## [Certificate Extraction](/docs/filescan/3.2.0/configuration/engine-config-basic-features#certificate-extraction)

Enable certificate extraction for executable files and PDF documents

transform.cfgCopyextractCertificates=true
checkCertificateRevocationMode=AUTO
osslExecutionTimeout=30

| Property name | Default value | Description |
| --- | --- | --- |
| extractCertificates | true | Switch do enable / disable certificate extraction |
| checkCertificateRevocationMode | AUTO | ON - enabled OFF - disabled AUTO - will be set based on other configurations |
| osslExecutionTimeout | 30 seconds | Execution timeout |

## [YARA](/docs/filescan/3.2.0/configuration/engine-config-basic-features#yara)

Enable YARA rule matching

transform.cfgCopyrunYaraRulesOnInputFile=true
runYaraRulesOnExtractedFiles=true
yaraExecutionTimeout=30
runYaraRulesOnInputFileMaxFileSizeInMb=100

| Property name | Default value | Description |
| --- | --- | --- |
| runYaraRulesOnInputFile | true | Switch to enable / disable YARA rule matching |
| runYaraRulesOnExtractedFiles | true | Execute YARA also on extracted files |
| yaraExecutionTimeout | 30 seconds | Execution timeout |
| runYaraRulesOnInputFileMaxFileSizeInMb | 100 MB | File size limit, '0' means no limit |

## [Image Text Extraction (OCR)](/docs/filescan/3.2.0/configuration/engine-config-basic-features#image-text-extraction-ocr)

Enable text extraction from images

transform.cfgCopyrunTesseractOCRForImages=true
tesseractExecutionTimeout=10
tesseractLimitPerTransform=5

| Property name | Default value | Description |
| --- | --- | --- |
| runTesseractOCRForImages | true | Switch to enable / disable OCR |
| tesseractExecutionTimeout | 10 seconds | Execution timeout |
| tesseractLimitPerTransform | 5 | Limit: number of images to process |

## [QR Code Scan](/docs/filescan/3.2.0/configuration/engine-config-basic-features#qr-code-scan)

Enable QR code scan for images

transform.cfgCopyrunQRCodeScanForImages=true
qrCodeScanLimitPerTransform=20

| Property name | Default value | Description |
| --- | --- | --- |
| runQRCodeScanForImages | true | Switch to enable / disable QR code scanning |
| qrCodeScanLimitPerTransform | 20 | Limit: number of images to process |

## [Text Metrics](/docs/filescan/3.2.0/configuration/engine-config-basic-features#text-metrics)

transform.cfgCopygenerateTextMetrics=true
generateTextMetricsNGramSize=5
generateTextMetricsIncludeTopNGrams=20

Enable text metrics generation like entropy, average word size, etc.

| Property name | Default value | Description |
| --- | --- | --- |
| generateTextMetrics | true | Enable / disable text metrics generation |
| generateTextMetricsNGramSize | 5 | Size of collected ngrams |
| generateTextMetricsIncludeTopNGrams | 20 | Number of considered ngrams |

## [Visualization](/docs/filescan/3.2.0/configuration/engine-config-basic-features#visualization)

Enable image rendering of input file (file preview pages)

transform.cfgCopyrunFileVisualizer=true
runFileVisualizerTimeoutMs=10000

| Property name | Default value | Description |
| --- | --- | --- |
| runFileVisualizer | true | Switch to enable / disable visualization |
| runFileVisualizerTimeoutMs | 10 seconds | Execution timeout |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

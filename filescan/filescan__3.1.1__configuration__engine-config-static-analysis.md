<!-- source: https://www.opswat.com/docs/filescan/3.1.1/configuration/engine-config-static-analysis -->

# Static Analysis

**Step #1 - Open** `/home/sandbox/sandbox/transform.cfg` **in a text editor**

**Step #3 - Save the file and restart the** `sandbox` **service**

## [URLs](/docs/filescan/3.1.1/configuration/engine-config-static-analysis#urls)

Enable domain resolver, [IP stack](https://ipstack.com/) Geolocation and [Hexillion WHOIS](https://hexillion.com/) domain lookups

Info

[IP Geolocation lookup](https://docs.opswat.com/filescan/configuration/ip-geolocation) will be executed on resolved domains

transform.cfgCopyrunDomainResolver=true
domainResolveMaxResolves=20
runDomainResolveTimeoutMs=60000

| Property name | Default value | Description |
| --- | --- | --- |
| runDomainResolver | true | Switch to enable / disable domain resolving |
| domainResolveMaxResolves | 20 | Domain resolver limit, '0' means no limit |
| runDomainResolveTimeoutMs | 1 minute | Execution timeout |

transform.cfgCopyrunWhoisRecordLookups=true
runHexillionLookupTimeoutMs=30000
runHexillionLookupMaxLookups=30
hexillionUrl=https://hexillion.com/rf/xml/1.0/whois/?query=$domain
hexillionUsername=
hexillionPassword=

| Property Name | Default Value | Description |
| --- | --- | --- |
| runWhoisRecordLookups | true | Switch to enable / disable WHOIS lookups |
| runHexillionLookupTimeoutMs | 30 seconds | Execution timeout |
| runHexillionLookupMaxLookups | 30 | Lookup limit, '0' means no limit |
| hexillionUrl | <https://hexillion.com/rf/xml/1.0/whois/?query=$domain> | API URL |
| hexillionUsername |  | API username |
| hexillionPassword |  | API password |

## [Office Documents](/docs/filescan/3.1.1/configuration/engine-config-static-analysis#office-documents)

Enable static analysis for Microsoft Office documents

transform.cfgCopyrunContentParser=true
runContentParserDirectTimeoutMs=10000

| Property name | Default value | Description |
| --- | --- | --- |
| runContentParser | true | Switch to enable / disable Office document static analysis |
| runContentParserDirectTimeoutMs | 10 seconds | Execution timeout |

## [OLE Files](/docs/filescan/3.1.1/configuration/engine-config-static-analysis#ole-files)

Enable parsing OLE files

transform.cfgCopyrunOledumpOnOLEFiles=true
runOledumpBiffOnXLSFiles=true
oledumpExecutionTimeout=30
oledumpMaxFileSizeInKb=1024

| Property name | Default value | Description |
| --- | --- | --- |
| runOledumpOnOLEFiles | true | Switch to enable / disable OLE parsing |
| runOledumpBiffOnXLSFiles | true | Enable or disable parsing of BIFF records |
| oledumpExecutionTimeout | 30 seconds | Execution timeout |
| oledumpMaxFileSizeInKb | 1 MB | File size limit |

## [PE Files](/docs/filescan/3.1.1/configuration/engine-config-static-analysis#pe-files)

Enable executable file parsing, unpacking and disassembly

transform.cfgCopy# UPX unpacking
runUpxUnpacker=true
# Unipacker
runUnipackerOnPEFiles=true
unipackerExecutionTimeout=50
unipackerIgnorePackers=delphi,nullsoft
unipackerMaxFileSizeInKb=2048
# AutoIt unpacking
runAutoItRipper=true
# Python unpacking
runPythonUnpacker=true
pythonUnpackerTimeout=30
# Disassembly
extractDisassemblySections=true
extractDisassemblySectionsLimit=200
extractDisassemblySectionsInstructionLimit=10000
# .NET unpacking
runDe4DotForNetFiles=true
de4dotExecutionTimeout=30
# Detect it easy
enableDetectItEasy=true
enableDetectItEasyForExtractedFiles=true
detectItEasyTimeout=3

| Property name | Default value | Description |
| --- | --- | --- |
| runUpxUnpacker | true | Switch to enable / disable UPX unpacking |

| Property name | Default value | Description |
| --- | --- | --- |
| runUnipackerOnPEFiles | true | Switch to enable / disable unpacking |
| unipackerExecutionTimeout | 50 seconds | Execution timeout |
| unipackerIgnorePackers | delphi,nullsoft | Comma separated list of ignored unpackers |
| unipackerMaxFileSizeInKb | 2 MB | File size limit |

| Property name | Default value | Description |
| --- | --- | --- |
| runAutoItRipper | true | Switch to enable / disable AutoItRipper, extraction of compiled AutoIt scripts |

| Property name | Default value | Description |
| --- | --- | --- |
| runPythonUnpacker | true | Switch to enable / disable Python unpacking |
| pythonUnpackerTimeout | 30 seconds | Switch to enable / disable Python unpacking, extraction of compiled Python scripts |

| Property name | Default value | Description |
| --- | --- | --- |
| extractDisassemblySections | true | Switch to enable / disable disassembly |
| extractDisassemblySectionsLimit | 200 | Limit: the number of disassembled sections |
| extractDisassemblySectionsInstructionLimit | 10000 | Limit: the number of disassembled instructions |

| Property name | Default value | Description |
| --- | --- | --- |
| runDe4DotForNetFiles | true | Switch to enable / disable .NET unpacking |
| de4dotExecutionTimeout | 30 seconds | Execution timeout |

| Property name | Default value | Description |
| --- | --- | --- |
| enableDetectItEasy | true | Switch to enable / disable DetectItEasy, file type and attribute detection |
| enableDetectItEasyForExtractedFiles | true | Enable DetectItEasy on extracted files |
| detectItEasyTimeout | 3 seconds | Execution timeout |

## [Android Files](/docs/filescan/3.1.1/configuration/engine-config-static-analysis#android-files)

Enable Android APK parsing

transform.cfgCopyrunAPKToolForAndroidFiles=true
apkToolExecutionTimeout=60
apkToolParseMaxFolderDepth=10
apkToolCheckMaxFiles=10000
apkToolParseMaxFiles=1000

| Property name | Default value | Description |
| --- | --- | --- |
| runAPKToolForAndroidFiles | true | Switch to enable / disable APK parsing |
| apkToolExecutionTimeout | 60 seconds | Execution timeout |
| apkToolParseMaxFolderDepth | 10 | Limit: APK archive folder dept |
| apkToolCheckMaxFiles | 10000 | Limit: APK archive file count |
| apkToolParseMaxFiles | 1000 | Limit: Smali file count |

## [Java Files](/docs/filescan/3.1.1/configuration/engine-config-static-analysis#java-files)

Enable Java decompilation

transform.cfgCopyrunCFRForJavaFiles=true
cfrExecutionTimeout=30

| Property name | Default value | Description |
| --- | --- | --- |
| runCFRForJavaFiles | true | Switch to enable / disable Java decompilation |
| cfrExecutionTimeout | 30 seconds | Execution timeout |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

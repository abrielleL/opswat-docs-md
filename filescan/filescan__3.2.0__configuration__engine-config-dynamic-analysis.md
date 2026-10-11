<!-- source: https://www.opswat.com/docs/filescan/3.2.0/configuration/engine-config-dynamic-analysis -->

# Dynamic Analysis

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Adaptive Sandbox dynamic analysis features

**Step #1 - Open** `/home/sandbox/sandbox/transform.cfg` **in a text editor**

**Step #3 - Save the file and restart the** `sandbox` **service**

## [Phishing Detection](/docs/filescan/3.2.0/configuration/engine-config-dynamic-analysis#phishing-detection)

transform.cfgCopyrunAnesidoraWebForURLToFileSubmissions=true
runAnesidoraWebLookupTimeoutMs=60000

| Property Name | Default Value | Description |
| --- | --- | --- |
| runAnesidoraWebForURLToFileSubmissions | true | Switch to enable / disable phishing detection |
| runAnesidoraWebLookupTimeoutMs | 1 minute | Execution timeout |

## [Script Emulation](/docs/filescan/3.2.0/configuration/engine-config-dynamic-analysis#script-emulation)

Enable JScript, VBScript, HTA/MSHTA and Powershell script emulation

BashCopyrunVBADecoderForOfficeFiles=true
runVBADecoderForPdfFiles=true
runVBADecoderForScriptFiles=true
runVBADecoderForHtmlFiles=true
runVBADecoderForExtractedFiles=true
runVBADecoderForDownloadedFiles=true
anesidoraVBAPerformDeepStaticAnalysisForExtractedFiles=true
anesidoraVBAPerformDeepStaticAnalysisForExtractedFilesMax=10
anesidoraVBAPerformDeepStaticAnalysisForExtractedFilesMaxSizeInKb=1024
anesidoraVBAExecutionTimeout=90

| Property Name | Default Value | Description |
| --- | --- | --- |
| runVBADecoderForOfficeFiles | true | Switch to enable / disable Office file emulation |
| runVBADecoderForPdfFiles | true | Switch to enable / disable PDF file emulation |
| runVBADecoderForScriptFiles | true | Switch to enable / disable script file emulation |
| runVBADecoderForHtmlFiles | true | Switch to enable / disable HTML file emulation |
| runVBADecoderForExtractedFiles | true | Emulate extracted files |
| runVBADecoderForDownloadedFiles | true | Emulate downloaded files |
| anesidoraVBAExecutionTimeout | 90 seconds | Execution timeout |
| anesidoraVBAPerformDeepStaticAnalysisForExtractedFiles | true | Execute static analysis on extracted files detected during emulation |
| anesidoraVBAPerformDeepStaticAnalysisForExtractedFilesMax | 10 | Limit: the max number of files execute static analysis on |
| anesidoraVBAPerformDeepStaticAnalysisForExtractedFilesMaxSizeInKb | 1 MB | Limit: the max size of files execute static analysis on |

## [PE Emulation](/docs/filescan/3.2.0/configuration/engine-config-dynamic-analysis#pe-emulation)

Enable Portable Executable emulation

Warning

This is an experimental feature

transform.cfgCopyrunPEEmulator=false
peEmuEmulatePEFiles=true
peEmuEmulateRawShellcode=true
pEEmuExecutionTimeout=90
pEEmuPerformDeepStaticAnalysisForExtractedFiles=true
pEEmuPerformDeepStaticAnalysisForExtractedFilesMax=10
pEEmuIgnoreClueTypes=SessionStarted,EmulationEnd,Exception,UnhandledAPI
pEEmuConfigFile.Unix=

| Property Name | Default Value | Description |
| --- | --- | --- |
| runPEEmulator | true | Main switch to enable / disable PE emulation |
| peEmuEmulatePEFiles | true | Switch to enable / disable PE emulation for PE files |
| peEmuEmulateRawShellcode | true | Switch to enable / disable PE emulation for raw shellcode |
| pEEmuExecutionTimeout | 90 seconds | Execution timeout |
| pEEmuPerformDeepStaticAnalysisForExtractedFiles | true | Execute emulation on extracted files |
| pEEmuPerformDeepStaticAnalysisForExtractedFilesMax | 10 | Limit: max number of extracted files to emulate |
| pEEmuIgnoreClueTypes | SessionStarted, EmulationEnd, Exception, UnhandledAPI | Emulation events to be ignored by the sandbox |
| pEEmuConfigFile.Unix |  | Use the specific config file to modify API tracing filter and other PE emulator parameters |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

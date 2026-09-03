<!-- source: https://www.opswat.com/docs/filescan/3.1.1/datasheet/supported-file-types -->

# Supported File Types

MetaDefender Aether accepts files below the size limit for analysis. The table below lists the most prevalent file types officially supported, organized by category. Unlisted file types may yield less accurate analysis results.

## [Application Files](/docs/filescan/3.1.1/datasheet/supported-file-types#application-files)

| File Type | **Static Analysis** | **Dynamic Analysis** | OS | **Comment** |
| --- | --- | --- | --- | --- |
| A3X | Yes | No | Windows | AutoIt v3 Script |
| AU3 | Yes | No | Windows | AutoIt v3 Script |

## [Office Documents](/docs/filescan/3.1.1/datasheet/supported-file-types#office-documents)

| File Type | **Static Analysis** | **Dynamic Analysis** | OS | **Comment** |
| --- | --- | --- | --- | --- |
| DOCX | Yes | Yes | Windows | Microsoft Word Document (.docx) |
| DOCM | Yes | Yes | Windows | Microsoft Word Macro-Enabled Document (.docm) |
| DOTX | Yes | Yes | Windows | Microsoft Word Template (.dotx) |
| DOTM | Yes | Yes | Windows | Microsoft Word Macro-Enabled Template (.dotm) |
| DOC | Yes | Yes | Windows | Microsoft Word 97-2003 Document (.doc) |
| DOT | Yes | Yes | Windows | Microsoft Word 97-2003 Template (.dot) |
| XLSX | Yes | Yes | Windows | Microsoft Excel Workbook (.xlsx) |
| XLSB | Yes | Yes | Windows | Microsoft Excel Binary Workbook |
| XLSM | Yes | Yes | Windows | Microsoft Excel Macro-Enabled Workbook (.xlsm) |
| XLS | Yes | Yes | Windows | Microsoft Excel 97-2003 Workbook (.xls) |
| XLTX | Yes | Yes | Windows | Microsoft Excel Template (.xltx) |
| XLTM | Yes | Yes | Windows | Microsoft Excel Macro-Enabled Template (.xltm) |
| PPTX | Yes | Yes | Windows | Microsoft PowerPoint Presentation (.pptx) |
| PPTM | Yes | Yes | Windows | Microsoft PowerPoint Macro-Enabled Presentation (.pptm) |
| PPSX | Yes | Yes | Windows | Microsoft PowerPoint Slide Show (.ppsx) |
| PPT | Yes | Yes | Windows | Microsoft PowerPoint 97-2003 Presentation (.ppt) |
| PPAM | Yes | Yes | Windows | Microsoft PowerPoint Add-in |
| POTX | Yes | Yes | Windows | Microsoft PowerPoint Template |
| POTM | Yes | Yes | Windows | Microsoft PowerPoint Macro-Enabled Template |
| POT | Yes | Yes | Windows | Microsoft PowerPoint 97-2003 Template |
| ODT | Yes | No | Multi-OS | OpenDocument Text |
| ODS | Yes | No | Multi-OS | OpenDocument Spreadsheet |
| RTF | Yes | Yes | Windows | Rich Text Format |
| HWP | Yes | Yes | Windows | Hangul Word Processor |
| PUB | Yes | Yes | Windows | Microsoft Publisher |
| ONE | Yes | Yes, limited* | Windows | Microsoft OneNote exported section |
| DOC95 | Yes | No | Windows | Microsoft Word 95 Document (.doc) |
| DOT95 | Yes | No | Windows | Microsoft Word 95 Template (.dot) |
| XLS95 | Yes | No | Windows | Microsoft Excel 95 Workbook (.xls) |
| PPT95 | Yes | No | Windows | Microsoft PowerPoint 95 Presentation (.ppt) |
| ODC | Yes | No | Multi-OS | Office Data Connection |
| ODF | Yes | No | Multi-OS | OpenDocument Formula |
| ODG | Yes | No | Multi-OS | OpenDocument Graphics |
| ODI | Yes | No | Multi-OS | OpenDocument Image |
| ODP | Yes | No | Multi-OS | OpenDocument Presentation |
| XLM | Yes | Yes | Windows | Microsoft Excel 4.0 Macro sheet |
| XLT | Yes | Yes | Windows | Microsoft Excel Template |

## [Encrypted Documents](/docs/filescan/3.1.1/datasheet/supported-file-types#encrypted-documents)

Note

Encrypted documents are handled with special processing to extract and analyze content while maintaining security protocols.

## [Executable Files](/docs/filescan/3.1.1/datasheet/supported-file-types#executable-files)

| File Type | **Static Analysis** | **Dynamic Analysis** | OS | **Comment** |
| --- | --- | --- | --- | --- |
| PE (EXE/DLL) | Yes | Yes, limited** | Windows | PE unpacking & re-analysis. Beta PE emulator available for 32-bit EXE files. |
| PE (dotnet_pe) | Yes | Yes, limited** | Windows | PE.NET decompilation & re-analysis. (Not emulated) |
| PE (other) | Yes | Yes, limited** | Windows | Other specific PE types (SFX, Golang, Rust, etc.) |
| APK | Yes | No | Android | Android Application Package |
| CPL | Yes | No | Windows | Control Panel Extension |
| ELF | Yes | No | Unix | Executable and Linkable Format |
| LNK | Yes | Yes | Windows | Windows Shortcut |
| MSI | Yes | No | Windows | Windows Installer Package |

## [Installers](/docs/filescan/3.1.1/datasheet/supported-file-types#installers)

| File Type | **Static Analysis** | **Dynamic Analysis** | OS | **Comment** |
| --- | --- | --- | --- | --- |
| Actual Installer | Yes | No | Windows | Actual Installer |
| Advanced Installer | Yes | No | Windows | Advanced Installer Project |
| Inno Setup | Yes | No | Windows | Inno Setup |
| Install Anywhere | Yes | No | Windows | Install Anywhere |
| InstallShield | Yes | No | Windows | InstallShield |
| MSI | Yes | No | Windows | Windows Installer Package |
| NSIS | Yes | No | Windows | Nullsoft Scriptable Install System |
| Wise Installer | Yes | No | Windows | Wise Installer |
| WiX | Yes | No | Windows | Windows Installer XML |

## [Image Files](/docs/filescan/3.1.1/datasheet/supported-file-types#image-files)

| File Type | **Static Analysis** | **Dynamic Analysis** | OS | **Comment** |
| --- | --- | --- | --- | --- |
| BMP | Yes | No | Multi-OS | Hidden data checks |
| DWG | Yes | No | Windows | VBA macro extraction |
| JPG | Yes | No | Multi-OS | Hidden data checks |
| PNG | Yes | No | Multi-OS | Hidden data checks |
| SVG | Yes | Yes, limited* | Windows | Scalable Vector Graphics |

## [Disk Image Files](/docs/filescan/3.1.1/datasheet/supported-file-types#disk-image-files)

Note

Disk image files are analyzed for contained file systems and embedded content.

## [Media Files](/docs/filescan/3.1.1/datasheet/supported-file-types#media-files)

| File Type | **Static Analysis** | **Dynamic Analysis** | OS | **Comment** |
| --- | --- | --- | --- | --- |
| ASF | Yes | No | Windows | Windows Media Video |
| MP3 | Yes | No | Multi-OS | MPEG-1 Audio Layer-3 |
| WMV | Yes | No | Multi-OS | Metadata analysis |

## [Other](/docs/filescan/3.1.1/datasheet/supported-file-types#other)

| File Type | **Static Analysis** | **Dynamic Analysis** | OS | **Comment** |
| --- | --- | --- | --- | --- |
| CHM | Yes | Yes | Windows | Compiled HTML Help |
| CLASS (java-bytecode) | Yes | No | Multi-OS | Limited support. Yet just for a few specific malware config extraction |
| Java | Yes | No | Multi-OS | Java Decompilation & re-analysis |
| H5 | Yes | No | Multi-OS | Keras, HDF5 format |
| MHT, MHTML | Yes | No | Multi-OS | Web Archive |
| MSC | Yes | Yes | Windows | Microsoft Management Console |
| MSO | Yes | Yes | Multi-OS | Microsoft office active/macro object files |
| OLE | Yes | Yes | Windows | Object Linking and Embedding |
| Pickle | Yes | No | Multi-OS | Python Pickle |
| PyTorch | Yes | No | Multi-OS | PyTorch Models |
| SCT | Yes | Yes | Windows | Windows Scriptlet |
| PB | Yes | No | Multi-OS | Tensorflow, Protocol Buffers format |

## [Adobe Files](/docs/filescan/3.1.1/datasheet/supported-file-types#adobe-files)

| File Type | **Static Analysis** | **Dynamic Analysis** | OS | **Comment** |
| --- | --- | --- | --- | --- |
| PDF | Yes | Yes, limited* | Multi-OS | Portable Document Format |

## [Text Files](/docs/filescan/3.1.1/datasheet/supported-file-types#text-files)

| File Type | **Static Analysis** | **Dynamic Analysis** | OS | **Comment** |
| --- | --- | --- | --- | --- |
| HTML | Yes | Yes, limited* | Windows | Hypertext Markup Language |
| TXT | Yes | Yes | Windows | Plain Text |
| HTA | Yes | Yes | Windows | HTML Application |
| WSF | Yes | Yes | Windows | Windows Script File |
| BAT | Yes | Yes | Windows | Batch Script |
| JScript | Yes | Yes | Windows | Microsoft's implementation of JavaScript |
| JSE | Yes | Yes | Windows | JScript Encoded |
| PS1 | Yes | Yes | Windows | PowerShell |
| VBScript | Yes | Yes | Windows | Visual Basic Script |
| CSV | Yes | No | Multi-OS | Comma-Separated Values |
| ICS | Yes | No | Multi-OS | iCalendar |
| JS | Yes | Yes | Multi-OS | JavaScript |
| JSON | Yes | No | Multi-OS | JavaScript Object Notation |
| PY | Yes | No | Multi-OS | Python |
| SH | Yes | No | Unix | Shell script |
| XML | Yes | No | Multi-OS | Extensible Markup Language |
| PHP | Yes | No | Multi-OS | Hypertext Preprocessor |
| ASP | Yes | Yes | Multi-OS | Active Server Page |

## [Email Files](/docs/filescan/3.1.1/datasheet/supported-file-types#email-files)

| File Type | **Static Analysis** | **Dynamic Analysis** | OS | **Comment** |
| --- | --- | --- | --- | --- |
| EML | Yes | Yes, limited* | Windows | Electronic Mail |
| MBOX | Yes | Yes | Windows | Mailbox Format |
| MSG | Yes | No | Windows | Outlook Message |
| RFC822 | Yes | No | Windows | RFC822 Email Format |

## [Archive Files](/docs/filescan/3.1.1/datasheet/supported-file-types#archive-files)

| Supported Archive Types | Archives extraction | Type-specific analysis | Comment |
| --- | --- | --- | --- |
| 7Z | Yes | N/A |  |
| ACE | Yes | N/A |  |
| BZIP2/BZ2 | Yes | N/A |  |
| CAB | No | Yes | Requires version 1.6.1 or later |
| CRX |  |  | CRX (Google Chrome Extension) package |
| DEB | Yes* | Yes |  |
| GTAR | Yes | N/A |  |
| GZIP | Yes | N/A |  |
| LZIP | Yes | N/A |  |
| ISO | Yes | No |  |
| PKG (NodeJS) | Yes | No |  |
| RAR | Yes | N/A |  |
| SFX (PEEXE) | Yes | Yes |  |
| TBZ2 | Yes | N/A |  |
| TAR | Yes | N/A |  |
| TGZ | Yes | N/A |  |
| TXZ | Yes | N/A |  |
| MSU | Yes | No |  |
| VHD | Yes | N/A | Requires 1.6.3 or later |
| VSIX | Yes | N/A | VSIX (Visual Studio Extension) package |
| WHL | Yes | No |  |
| XPI | Yes | No |  |
| ZIP | Yes | N/A |  |
| ZIPX | Yes | N/A |  |

** The most relevant files are identified and extracted, along with the file list. But not all of the contained files.*

---

*Note: The MIME type is detected automatically regardless of the provided file suffix.*

** if the file contains objects that have dedicated dynamic analysis support (e.g. JavaScript in PDF)*

*** Read more about* [*supported unpackers*](https://docs.opswat.com/filescan/datasheet/supported-packers-for-unpacking) and full overview of executable capabilities available [here](https://docs.opswat.com/filescan/datasheet/executable-analysis)

#### [Maximum File Size:](/docs/filescan/3.1.1/datasheet/supported-file-types#maximum-file-size)

The maximum file size is 2000 MB.

*Note: All file size limits can be configured.*

#### [Maximum parallel uploads](/docs/filescan/3.1.1/datasheet/supported-file-types#maximum-parallel-uploads)

Maximum parallel uploads - as part of an archive - from v2.*.*:

- 1000 executables,
- 10 documents,
- 10 other

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

<!-- source: https://www.opswat.com/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud -->

# Data Sanitization on MetaDefender Cloud

## [MetaDefender Cloud Deep CDR](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#metadefender-cloud-deep-cdr)

[Data sanitization, also known as Deep Content Disarm and Reconstruction (CDR)](https://www.opswat.com/technologies/data-sanitization), is the process of breaking down a file, removing exploitable content, and then reconstructing the file with all original content and functionality restored. This process renders files safe by stripping potentially malicious or insecure content – macros and hyperlinks, for example.

## [How It Works](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#how-it-works)

MetaDefender Cloud sanitizes files after first scanning them for malware with 20+ anti-malware engines. After multiscanning is complete, MetaDefender Cloud creates a sanitized version of every file. The sanitized file is available for immediate download. To download the file, click "Sanitized File" above the displayed multiscanning results, then click "Download Sanitized."

Data sanitization (CDR) does not modify or alter the content within a file. It simply removes the exploitable objects within the file.

Our data sanitization (CDR) technology supports over 150 file types including common file types such as DOC(X), XLS (X), PPT(X), and PDF, and we are always adding more in order to expand the protection afforded by data sanitization.

The Deep CDR engine is always the latest version on MetaDefender Cloud. The engine configuration is standard and no file conversion is performed.

## [Supported File Types](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#supported-file-types)

|  | Source File Type | Description | Target Sanitized Types |
| --- | --- | --- | --- |
| 1 | doc | Microsoft Word 97-2003 Document | **doc**, docx, pdf, rtf |
| 2 | dot | Microsoft Word 97-2003 Template | **dot,** dotx |
| 3 | xls | Microsoft Excel 97-2003 Workbook | **xls**, pdf, csv |
| 4 | xlt | Microsoft Excel 97-2003 Template | **xlt**, `pdf` ,`png` |
| 5 | ppt | Microsoft PowerPoint 97-2003 Presentation | **ppt**, pdf |
| 6 | pot | Microsoft PowerPoint 97-2003 Template | **pot**, `pdf` ,`png` |
| 7 | rtf | Microsoft Rich Text Format | **rtf,** pdf |
| 8 | docx | Microsoft Word Document | **docx**, html, pdf, `ps, jpg, bmp, png, tiff, svg, rtf` |
| 9 | docm | Microsoft Word Macro-Enabled Document | **docm**, `docx, html, pdf, ps, jpg, bmp, png, tiff, svg` , rtf |
| 10 | dotx | Microsoft Word Template | **dotx** |
| 11 | dotm | Microsoft Word Macro-Enabled Template | **dotm** , dotx |
| 12 | xlsx | Microsoft Excel Workbook | **xlsx**, csv, html, `tiff, pdf, ps, jpg, bmp, png, svg` |
| 13 | xlsm | Microsoft Excel Macro-Enabled Workbook | **xlsm** , `xlsx, csv, html, tiff, pdf, ps, jpg, bmp, png, svg` |
| 14 | xlsb | Microsoft Excel Binary Workbook | **xlsb** |
| 15 | xltx | Microsoft Excel Template | **xltx**, `pdf, png` , csv |
| 16 | xltm | Microsoft Excel Macro-Enabled Template | **xltm**, `pdf, png` , csv |
| 17 | csv | Comma-separated values | **csv** |
| 18 | tsv | Tab-separated values | **tsv** |
| 19 | pptx | Microsoft PowerPoint Presentation | **pptx**, `html, pdf, ps, jpg` , bmp, `png, tiff, svg` |
| 20 | potx | Microsoft PowerPoint Template | **potx**, `pdf, png` |
| 21 | pptm | Microsoft PowerPoint Macro-Enabled Presentation | **pptm** , `pptx, html, pdf, ps, jpg, bmp, png, tiff, svg` |
| 22 | potm | Microsoft PowerPoint Macro-Enabled Template | **potm**, `pdf, png` |
| 23 | pps | Microsoft PowerPoint 97-2003 Show | **pps**, `pdf, png` |
| 24 | ppsm | Microsoft PowerPoint Macro-Enabled Show | **ppsm**, `pdf, png` |
| 25 | ppsx | Microsoft PowerPoint Show | **ppsx,** bmp |
| 26 | ppam | Microsoft Powerpoint add-on | **ppam** |
| 27 | sldx | Microsoft Powerpoint Slide 2007+ | **sldx** |
| 28 | sldm | Microsoft Office PowerPoint 2007 Slide - Macro Enabled | **sldm** |
| 29 | vsdx | Microsoft Visio Drawing | **vsdx**, `pdf, xps, jpg, png, bmp, tiff, svg, emf*, html, xaml, swf` |
| 30 | vssx | Microsoft Visio Stencil | **vssx**, `pdf, xps, jpg, png, bmp, tiff, svg, emf, html, xaml, swf` |
| 31 | vstx | Microsoft Visio Template | **vstx**, `pdf, xps, jpg, png, bmp, tiff, svg, emf, html, xaml, swf` |
| 32 | vsdm | Microsoft Visio Macro-Enabled Drawing | **vsdm**, `pdf, xps, jpg, png, bmp, tiff, svg, emf, html, xaml, swf` |
| 33 | vssm | Microsoft Visio Macro-Enabled Stencil | **vssm**, `pdf, xps, jpg, png, bmp, tiff, svg, emf, html, xaml, swf` |
| 34 | vstm | Microsoft Visio Macro-Enabled Template | **vstm**, `pdf, xps, jpg, png, bmp, tiff, svg, emf, html, xaml, swf` |
| 35 | vsx | Microsoft Visio XML Stencil | **vsx**, `pdf, xps, jpg, png, bmp, tiff, svg, emf, html, xaml, swf` |
| 36 | vtx | Microsoft Visio XML Template | **vtx**, `pdf, xps, jpg, png, bmp, tiff, svg, emf, html, xaml, swf` |
| 37 | vtx | Microsoft Visio XML Template | **vtx**, `pdf, xps, jpg, png, bmp, tiff, svg, emf, html, xaml, swf` |
| 38 | one | Microsoft OneNote | **one** |
| 39 | odt | OpenDocument Text | **odt** |
| 40 | ods | OpenDocument Spreadsheet | **ods** |
| 41 | ott | OpenDocument Document Template | **ott** |
| 42 | ots | OpenDocument Spreadsheet Template | **ots** |
| 43 | odp | OpenDocument Presentation | **odp** |
| 44 | otp | OpenDocument Presentation Template | **otp** |
| 45 | htm/html | Hypertext Markup Language | **html**, `pdf, ps, jpg, bmp, png, svg` |
| 46 | mht | MIME HTML | **pdf**, `pg, bmp, png, tiff` |
| 47 | hta | HTML Application | **hta** |
| 48 | pdf | Adobe Portable Document Format | **pdf**, `html, svg, jpg, bmp, png, tiff` |
| 49 | hta | HTML Application | **hta** |
| 50 | pdf | Adobe Portable Document Format | **pdf**, `html, svg, jpg, bmp, png, tiff` |
| 51 | ai | Adobe Illustrator | **ai** |
| 52 | hwp | Hangul Word Processor | **hwp** |
| 53 | hwt | Hangul Word Template | **hwt** |
| 54 | hwpx | Hangul Word Processor | **hwpx** |
| 55 | cell | Hancom Cell | **cell** |
| 56 | show | Hancom Show | **show** |
| 57 | jtd | Ichitaro Document | **jtd** |
| 58 | jtdc | Ichitaro Compressed Document | **jtdc** |
| 59 | jhd | Justsystem Hanako | **jhd** |
| 60 | xml | Extensible Markup Language | **xml** |
| 61 | xml-doc | Microsoft Word 2003 XML Document | **pdf** |
| 62 | xml-docx | Microsoft Word XML Document | **xml-docx,** pdf |
| 63 | xml-xls | Microsoft XML Spreadsheet 2003 | **pdf** |
| 64 | twbx | Tableau packaged workbook | **twbx** |
| 65 | twb | Tableau workbook | **twb** |
| 66 | tds | Tableau Datasource | **tds** |
| 67 | rdf | Resource Description Framwork | rdf |
| 68 | vcs | vCalendar | **vcs** |
| 69 | ics | iCalendar | **ics** |
| 70 | lnk | Windows Shortcut | **lnk** |
| 71 | jpg | JPEG Image | **jpg**, bmp, png, tiff, svg, gif, ps, eps, pdf |
| 72 | jpx | JPEG 2000 | **jpx** |
| 73 | bmp | Windows Bitmap Image | **bmp**, jpg, png, tiff, svg, gif, ps, eps, pdf |
| 74 | png | Portable Network Graphics | **png**, jpg, bmp, tiff, svg, gif, ps, eps, pdf |
| 75 | apng | Animated PNG | **apng,** png |
| 76 | tiff | Tagged Image File Format | **tiff**, jpg, bmp, png, svg, gif, ps, eps |
| 77 | tiff64 | Big Tiff | **tiff64**, jpg, png, gif, bmp |
| 78 | nef | Nikon Raw Image | **nef**, jpg, bmp, png, svg, gif |
| 79 | svg | Scalable Vector Graphics |  |
| 80 | gif | Graphics Interchange Format | **gif,** jpg, bmp, png, tiff, svg, ps, eps, pdf |
| 81 | wmf | Windows Metafile | **wmf**, `jpg, bmp, png, tiff, svg, gif, ps,eps, pdf` |
| 82 | emf | Windows Enhanced Metafile | **emf** |
| 83 | ico | Icon | **ico** |
| 84 | cur | Cursor | **cur** |
| 85 | webp | Google Image File Format for Web | **webp** |
| 86 | wdp | HD Photo | **wdp** |
| 87 | dwg | AutoCAD | **dwg** |
| 88 | dwt | AutoCAD Drawing Template | **dwt** |
| 89 | dws | AutoCAD Drawing Standards | **dws** |
| 90 | sfc | SXF Feature Comment | **sfc** |
| 91 | p21 | STEP Data Model | **p21** |
| 92 | jww | JW CAD | **jww** |
| 93 | jwc | JW CAD | **jwc** |
| 94 | bfo | V-nas BFO | **bfo** |
| 95 | dxf | AutoCAD DXF | dxf, **pdf**, `jpg, png, bmp, gif, tiff` |
| 96 | dwf | Design Web Format | **dwf,** pdf, `jpg, png, bmp, gif, tiff` |
| 97 | 3ds | 3D Studio | **3ds**, `dae, stl, fbx` |
| 98 | dae | Digital Asset Exchange | **dae**, `3ds, stl, fbx` |
| 99 | u3d | Universal 3D | **u3d**, `3ds, dae, stl, pdf, drc, rvm, fbx` |
| 100 | drc | Google Draco | **drc**, `3ds, dae, pdf, u3d, rvm, fbx` |
| 101 | rvm | AVEVA Plant Design Management System Model | **rvm**, `3ds, dae, stl, pdf, u3d, drc, fbx` |
| 102 | dcm | Digital Imaging and Communications in Medicine | **dcm** |
| 103 | shp | Shapefile | **shp** |
| 104 | shx | Shapefile | **shx** |
| 105 | wmv | Windows Media Video | **wmv** |
| 106 | wma | Windows Media Audio | **wma** |
| 107 | mpeg | Moving Picture Experts Group | **mpeg** |
| 108 | wav | Waveform Audio | **wav** |
| 109 | mp3 | MPEG-1 Audio Layer-3 | **mp3** |
| 110 | mp4 | MPEG-4 Part 14 | **mp4** |
| 111 | mov | QuickTime video format | **mov** |
| 112 | avi | Audio Video Interleave | **avi** |
| 113 | webm | Video file format | **webm** |
| 114 | flv | Flash Video | **flv** |
| 115 | bwf | Broadcast wave format | **bwf** |
| 116 | w64 | Sony wave64 autdio format | **w64** |
| 117 | rf64 | BWF-compatible multichannel audio file format | **rf64** |
| 118 | m4a | MPEG-4 Audio | **m4a** |
| 119 | mts | MPEG-2 Tranmission | **m2s** |
| 120 | ogg | Ogg Vorbis Compressed Audio | **ogg** |
| 121 | aiff | Audio Interchange File Forma | **aiff** |
| 122 | aac | Advanced Audio Coding | **aac** |
| 123 | opus | Ogg Opus | **opus** |
| 124 | mxf | Material Exchange Format | **mxf** |
| 125 | vtxt | VTXT | **vtxt** |
| 126 | eml | Electronic mail | **eml** |
| 127 | msg | Microsoft Outlook Message | **msg** |
| 128 | oft | Microsoft Outlook Template | **oft** |
| 129 | pst | Outlook Personal Folder | **pst** |
| 130 | json | JSON | **json** |
| 131 | xdw | DocuWork Image | **xdw** |
| 132 | xbd | DocuWork Binder | **xbd** |
| 133 | xct | DocuWork Container | **xct** |
| 134 | crl | Certificate Revocation List | **crl** |
| 135 | spf | StorageCraft ShadowProtect | **spf** |
| 136 | utib | UTIB | **utib** |
| 137 | har | HTML Archive | **har** |
| 138 | story | Storyist Document | **story** |
| 139 | 7z | 7-zip Archive | **7z**, zip, gz, xz, tar |
| 140 | gz/gzip | GNU Zipped Archive | **gz**, 7z, zip, xz, tar |
| 141 | rar | WinRAR Archive | **rar,** zip, 7z, gz, xz, tar |
| 142 | xz | XZ Archive | **xz**, zip, 7z, gz, tar |
| 143 | zip | ZIP Archive | **zip**, 7z, gz, xz, tar |
| 144 | alz | ALZip | **zip**, 7z, gz, xz, tar |
| 145 | tar | Tape Archive | **tar,** zip, 7z, gz, xz |
| 146 | bz2 | BZ2 Archive | **zip**, 7z, gz, xz, tar |
| 147 | lzma | LZMA Archive | **zip**, 7z, gz, xz, tar |
| 148 | lzh | LZH Archive | **zip**, 7z, gz, xz, tar |
| 149 | tsec | TIP Test Selection Engine | **tsec**, zip, 7z, gz, xz, tar |
| 150 | egg | EGG archive format | **zip**, 7z, gz, xz, tar |
| 151 | asics | Associated Signature Container | **asics** |
| 152 | asice | Associated Signature Container | **asice** |
| 153 | es3 | e-dossier | **es3** |
| 154 | pck | System Center Configuration Manager Package Files | **pck** |
| 155 | aem | AppleSingle/AppleDouble Encoded Macintosh | **aem** |
| 156 | ribc | Research Institute on Building Cost | **ribc** |
| 157 | esz | E-szigno | **esz** |

## [How to Perform Deep CDR on Files](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#how-to-perform-deep-cdr-on-files)

In the UI, please make sure to enable "Deep CDR" on the advanced scanning menu:

## [Data Sanitization (CDR) APIs](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#data-sanitization-cdr-apis)

We offer a REST API for data sanitization (CDR) to allow users to incorporate the technology's capabilities into their own solutions.

Visit [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Data Sanitization Cdr) to learn more about this API.

## [Private Deep CDR](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#private-deep-cdr)

Whether uploading files in private mode or not the sanitized version of the file will be deleted after 24h.

## [Deep CDR Configuration - Advance settings](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#deep-cdr-configuration---advance-settings)

The table below explains how Deep CDR is configured on MetaDefender Cloud. This configuration is standard for all users and cannot be adapted to specific user needs.

Deep CDR is configured to keep the format of the original file (e.g: sanitized versions of PDFs will also be PDFs, we won’t convert them to images or any other format)

#### [Adobe](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#adobe)

| File Type | Remove Macro | Remove Embedded Object | Hyperlinks | Process Image | Remove Metadata | Remove Embedded Font | Remove Comments | Others |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PDF | yes | yes | remove | yes, also optimize size | no | no | no | Remove web content database, Process Form |

#### [Office Document](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#office-document)

| File Type | Remove Macro | Remove Embedded Object | Hyperlinks | Process Image | Remove Metadata | Remove Embedded Font | Remove Comments | Others |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Word | yes | yes | remove | yes | no | no | yes | Remove hidden text, Remove Custom XML, Cleanup unused resources |
| Excel | yes | yes | remove | yes | no | no | yes | Remove comment, Remove revision, Remove Custom XML, Cleanup unused resources, Remove external content |
| PPT | yes | yes | remove | yes | no | no | yes |  |
| ONE |  | yes |  | yes |  |  |  |  |
| RTF |  | yes |  | yes | no |  |  | Remove embedded html tags containing malicious nodes, Process font table, limit 4096 |
| Visio | yes | yes | remove | yes | no | yes |  |  |

#### [Image](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#image)

| File Type | Remove Macro | Remove Embedded Object | Hyperlinks | Process Image | Remove Metadata | Remove Embedded Font | Remove Comments | Others |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Image |  |  |  |  | yes |  |  | Remove ICC Profile, size limit 256mb, Sanitize QR code |
| SVG |  |  |  | yes |  |  |  | Remove JavaScript, CDATA, Injection, Process Embedded Image |
| DWG | yes |  |  |  |  |  |  |  |

#### [Open Office](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#open-office)

| File Type | Remove Macro | Remove Embedded Object | Hyperlinks | Process Image | Remove Metadata | Remove Embedded Font | Remove Comments | Others |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ODT | yes | yes | yes |  | yes | no | yes | Remove Hidden Text and Revisions |
| ODS | yes | yes | remove | yes | no | yes | yes |  |
| ODP | yes | yes | remove | yes | no | yes |  |  |

#### [Media](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#media)

| File Type | Remove Macro | Remove Embedded Object | Hyperlinks | Process Image | Remove Metadata | Remove Embedded Font | Remove Comments | Others |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MP3 |  |  |  |  | yes |  |  |  |
| AIFF | yes |  |  |  |  | yes |  |  |
| WAV |  |  |  |  | yes |  |  | Remove Hidden Data, and if removed, add random noise SNR 30dB |

#### [Japanese](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#japanese)

| File Type | Remove Macro | Remove Embedded Object | Hyperlinks | Process Image | Remove Metadata | Remove Embedded Font | Remove Comments | Others |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| JTD | yes | yes |  | yes |  | yes |  |  |
| SFC |  |  |  |  |  |  | yes |  |
| P21 |  |  |  |  |  |  | yes |  |
| JWW |  |  |  | yes |  |  |  |  |
| XDW |  | yes |  |  |  |  |  | Remove Image Annotation |

#### [Korean](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#korean)

| File Type | Remove Macro | Remove Embedded Object | Hyperlinks | Process Image | Remove Metadata | Remove Embedded Font | Remove Comments | Others |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Hancom cell | yes | yes | remove | yes | no |  | yes | Remove Revision |
| Hancom show | yes | yes | remove | yes | no |  | yes |  |
| Hangul Word Config (HWP) | yes | yes | remove | yes | no |  |  | Process RTF Document |

#### [Others](/docs/mdcloud/operation/data-sanitization-on-metadefender-cloud#others)

| File Type | Remove Macro | Remove Embedded Object | Hyperlinks | Process Image | Remove Metadata | Remove Embedded Font | Remove Comments | Others |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HTML |  | yes |  | yes |  |  | yes | Remove script, Applet, Iframe, Process zero font text, Process Form |
| XML | yes |  |  |  |  |  |  | Remove CDATA and injection |
| ICS |  |  |  |  |  |  |  | Sanitize Inline Attachment, remove if not supported. Remove External Attachments |
| HTA |  |  |  |  |  |  | yes | Remove Object, Remove Applet, Process Form, Remove Iframe, Process Embedded Image, Process zero font text |
| TWB | yes |  |  |  |  |  |  |  |

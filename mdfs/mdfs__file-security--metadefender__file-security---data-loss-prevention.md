<!-- source: https://www.opswat.com/docs/mdfs/file-security--metadefender/file-security---data-loss-prevention -->

# File Security - Data Loss Prevention

Cloud Security for Salesforce rolled out its latest Data Loss Prevention (DLP) feature. At the forefront of this enhancement is the Proactive DLP engine, designed to identify sensitive data within files.

### [Detect approach](/docs/mdfs/file-security--metadefender/file-security---data-loss-prevention#detect-approach)

To standout the capabilities of the Proactive DLP engine lies in its ability to identify and prevent the transmission of sensitive information within files, such as Credit Card Number and Social Security Numbers. The engine is compatible with various file formats, encompassing Microsoft Office documents and PDFs.

#### [Supported Sensitive Data](/docs/mdfs/file-security--metadefender/file-security---data-loss-prevention#supported-sensitive-data)

- Social Security Number (SSN, ITIN for US)
- Credit Card Number (CCN)
- Optical Character Recognition (OCR)
- IPv4
- Classless Inter-Domain Routing (CIDR)
- Detect Secrets from Cloud Providers: AWS, GCP, Microsoft Azure, IBM Cloud Platform
- Detect DB access: MySQL, PostgreSQL
- Detect Generic Private keys

Output filename format: originalfilename__proactive-dlp-processed_by_OPSWAT_MetaDefender*

_*_based on the configuration of the Sanitization option within OPSWAT - Settings page.

#### [Redact approach](/docs/mdfs/file-security--metadefender/file-security---data-loss-prevention#redact-approach)

When DLP is used together with Sanitization option, a new file will be generated and the sensitive data found will be automatically redacted*.

*through redaction, sensitive information, such as Credit Card Numbers (CCNs) and Social Security Numbers (SSNs), is concealed while preserving the overall structure and layout of the entire document. It's essential to emphasize that this approach ensures the privacy of the information while retaining the readability of the entire content.

### [Supported File Types](/docs/mdfs/file-security--metadefender/file-security---data-loss-prevention#supported-file-types)

#### [Text and Documents](https://www.opswat.com/docs/mdcloud/operation/proactive-data-loss-prevention--dlp-#text-and-documents)

- Ansi Text (*.txt)
- ASCII Text
- CSV (Comma-separated values) (*.csv)
- Tab-separated values (*.tsv)
- iCalendar (*.ics, *.vcs)
- Microsoft Excel for Mac 2.2, 3, 4, 5, 98, 2001, X, 2004, 2008, 2011
- Microsoft Excel for Windows 2, 3, 4, 5
- Microsoft Excel 95, 97, 2000, XP, 2003, 2007, 2010, 2013, 2016 (*.xls)
- Microsoft Excel Office Open XML 2007, 2010, 2013, and 2016 (*.xlsx)
- Microsoft Office Excel XML (*.xml)
- Microsoft PowerPoint 3, 4, 95, 97, 98, 2000, 2001, 2002, 2003, 2004, 2007, 2008, 2010, 2011, 2013, 2016 (*.ppt)
- Microsoft PowerPoint Office Open XML 2007, 2010, 2013, and 2016 (*.pptx)
- Microsoft PowerPoint 97-2003 Template (*.pot)
- Microsoft PowerPoint Template (*.potx)
- Microsoft PowerPoint Show (*.ppsx)
- Microsoft PowerPoint Macro-Enabled Presentation (*.pptm)
- Microsoft PowerPoint Macro-Enabled Show (*.ppsm)
- Microsoft PowerPoint Macro-Enabled Template (*.potm)
- Microsoft PowerPoint 97-2003 Show (*.pps)
- Microsoft Office PowerPoint XML (*.xml)
- Microsoft Rich Text Format (*.rtf)
- Microsoft Word for DOS 1, 2, 3, 4, 5, 6 (*.doc)
- Microsoft Word for Mac 1, 3, 4, 5, 6, 98, 2001, X, 2004, 2008, 2011
- Microsoft Word for Windows 1, 2, 6 (*.doc)
- Microsoft Word 95, 97, 98, 2000, 2002, 2003, 2007, 2010, 2013, 2016 (*.doc)
- Microsoft Word 2003 XML (*.xml)
- Microsoft Word Office Open XML 2007, 2010, 2013, 2016 (*.docx)
- Microsoft/Open XML Paper Specification (_.xps, ._oxps)
- Ichitaro Document (*.jtd)
- OpenOffice/LibreOffice versions 1, 2, 3, 4, and 5 documents, spreadsheets, and presentations (*.sxc, *.sxd, *.sxi, *.sxw, *.sxg, *.stc, *.sti, *.stw, *.stm, *.odt, *.ott, *.odg, *.otg, *.odp, *.otp, *.ods, *.ots, *.odf) (includes OASIS Open Document Format for Office Applications)
- PDF files (*.pdf), note: Encrypted PDF files cannot be indexed, unless the PDF file can be opened without a password and the PDF file permissions allow for text extraction.
- PDF Portfolio files (*.pdf), including embedded non-PDF documents.
- Unicode (UCS16, Mac or Windows byte order, or UTF-8)
- XML (*.xml)
- XML Schema Description Files (*.xsd)
- JSON (*.json)
- Python script, ASCII text executable (*.py)
- Artificial Intelligence Markup Language (*.aiml)
- Microsoft ASP.NET Web Form (*.aspx)
- PHP Hypertext Preprocessor (*.php)
- PowerShell Script (*.ps1)
- Atom web feed (*.atom)
- GPS eXchange Format (*.gpx)
- Resource Description Framework (*.rdf)
- Open Office XML Relationships (*.rels)
- RSS web feed (*.rss)
- Visual Basic Script Files (*.vbs)
- Compass and Ruler geometry (*.zir)
- Document Type Definition (*.dtd)
- Tableau Workbook (*.twb)
- Tableau Datasource (*.tds)
- Tableau Bookmark (*.tbm)
- Windows Script File (*.wsf)
- Bourne Again Shell (*.bash) Virtual Contact File (*.vcf)

#### [Email, HTML](https://www.opswat.com/docs/mdcloud/operation/proactive-data-loss-prevention--dlp-#email-html)

- EML (emails saved by Outlook Express) (*.eml)
- MSG (emails saved by Outlook), including attachments (*.msg)
- Eudora MBX message files (*.mbx)
- HTML (*.htm, *.html)
- MIME Encapsulation of Aggregate HTML Documents (.mht)
- Hypertext Markup Language Application (.hta)

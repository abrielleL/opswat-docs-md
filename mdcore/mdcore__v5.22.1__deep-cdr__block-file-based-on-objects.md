<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/deep-cdr/block-file-based-on-objects -->

# Block file based on objects

View as Markdown Ask ChatGPT about this page Ask Claude about this page

In some use cases, the sanitized file can't be used dues to an integrity check. We recommend to block file based on objects to prevent zero-day attack. To configure this feature, please follow these steps

- *Workflow Manageement > Workflows > Workflow name > Advanced >* Enable **Block file if containing**
- Enable the Object types you want to block and which file families should be blocked

If a file contains the blocked objects, MetaDefender Core will block the file with a new verdict - Blocked Verdict by Deep CDR - an example JSON result

BashCopy"process_info": {
"archive_handling_details": {},
"blocked_reason": "Blocked Verdict by Deep CDR",
"blocked_reasons": [
"Blocked Verdict by Deep CDR"
],
"file_type_skipped_scan": false,
"hash_time": 0,
"post_processing": {
"actions_failed": "",
"actions_ran": "Sanitized",
"converted_destination": "Test_sanitized_by_OPSWAT_MetaDefender_85fd41ae04704eab83895dd2e6a46685.docm",
"converted_to": "docm",
"copy_move_destination": "",
"sanitization_details": {
"description": "Sanitized successfully.",
"details": [
{
"action": "removed",
"count": 1,
"object_name": "macro"
}
],
"result_template_hash": "101e1f24371ac0133dcb46d3e801833230c9bbfec3db03b2bb62abc26e2a72c3",
"sanitized_file_info": {
"file_size": 10824,
"sha256": "ef09bf23546890751f888f2dc9f1cdcb21682597aea3d73a36d4b0fd4a5c8964"
},
"verdict": "blocked",
"verdict_explanations": [
"contain macro"
]
}
}

**Supported Category and File Family**

| **Object category** | **Included Object** | **Applicable file families** |
| --- | --- | --- |
| Script Object | Macro | Microsoft Office Word  Microsoft Office Excel  Microsoft Office Powerpoint  Open Document  Hancom  Ichitaro  Markup  Image  Visio  CAD  PDF |
|  | JavaScript | PDF  Markup  Image  Video |
|  | Script (Shell script, Script command) | Markup  Video |
|  | Document Open Action | PDF |
|  | Page Action | PDF |
|  | DDE | Markup  Microsoft Office Word  Microsoft Office Excel  RTF |
|  | VSTO macro | Microsoft Office Word  Microsoft Office Excel |
| Embedded Object | Embedded object | PDF  Markup  Visio  RTF  Ichitaro  Hancom  Open Document  Microsoft Office Word  Microsoft Office Excel  Microsoft Office Powerpoint |
|  | Embedded font | PDF  Microsoft Office Word  Microsoft Office Powerpoint  Open Document  Hancom  Ichitaro  RTF |
|  | Embedded image | Markup  Image |
|  | Embedded html | RTF |
|  | Attachment | PDF |
|  | OLE presentation | Hancom  Microsoft Office Word  Microsoft Office Excel  Microsoft Office Powerpoint |
|  | OLE | Microsoft Office Word  Microsoft Office Excel  Microsoft Office Powerpoint  Hancom  Open Document  Ichitaro  RTF  Visio  ONE |
|  | ActiveX control | Microsoft Office Word  Microsoft Office Excel  Microsoft Office Powerpoint |
|  | Binary data | Hancom  Microsoft Office Word  Microsoft Office Excel  Microsoft Office Powerpoint |
|  | Recursive object |  |
| External Content | External image | Image  Microsoft Office Word  Microsoft Office Excel  Microsoft Office Powerpoint  Hancom  Open Document |
|  | External video | Microsoft Office Word  Microsoft Office Powerpoint  Hancom |
|  | External content | PDF  Microsoft Office Word  Microsoft Office Excel |
|  | External attachment | Markup |
|  | External sheet | Microsoft Office Excel  Hancom |
| Hyperlink | Hyperlink | PDF  Microsoft Office Word  Microsoft Office Excel  Microsoft Office Powerpoint  Open Document  Hancom  Ichitaro  Markup  Visio  RTF  Text  ONE |
| Suspicious object | Suspicious stream (Suspicious streams in OLE structure, e.g., \u0005SebiesnrMkudrfcoIaamtykdDa in XLS or DOC_INFO in HWP.) | Microsoft Office Excel  Hancom |
|  | Suspicious node (Suspicious nodes like datastore or nodes starting with bin in RTF structure.) | RTF |
|  | Suspicious CDATA (`CDATA` nodes in XML structure.) | Markup  Image |
| Other risks | ActiveX command | Microsoft Office Powerpoint |
|  | ppaction protocol | Microsoft Office Powerpoint |

**Supported file type in file family**

| File family | Supported File type |
| --- | --- |
| Microsoft Office Word | doc, dot, docx, dotx, docm, dotm |
| Microsoft Office Powerpoint | ppt, pps, pot, pptx, pptm, ppsx, ppsm, potx, potm, sldx, sldm, ppam |
| Microsoft Office Excel | xls, xlt, xlsx, xlsm, xlsb, xltx, xltm |
| Markup | xml, twb, html, hta, ics, csv, tsv |
| Image | svg |
| RTF | rtf |
| Video | wmv |
| PDF | pdf, ai |
| Text | txt |
| CAD | dwg, dwt, dws |
| Open Document | odp, otp, ods, ots, odt, ott |
| Visio | vdx, vtx, vsx, vsdx, vstx, vssx, vsdm, vstm, vssm |
| Hancom | show, cell, hwp, hwt, hwpx |
| Ichitaro | jtd, jtdc, jhd |
| ONE | one |

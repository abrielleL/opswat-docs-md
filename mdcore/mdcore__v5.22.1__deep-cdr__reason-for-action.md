<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/deep-cdr/reason-for-action -->

# Reason for Action

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Some risk objects, like macros in MS Office, are easy to understand. However, there are many less obvious risk objects, such as document properties, template name, etc.... These properties allow users to input data, which can pose security risks. Deep CDR provides a "reason for action" for these objects, helping users better understand the associated risks.

**Supported reasons:**

| Action | Reason/Concern |
| --- | --- |
| Validate Document Properties | Free-form text fields can potentially allow attackers to input data that does not conform to Microsoft schemas.  Reference: [Inspection and Sanitization Guide (ISG)](https://github.com/OpenSecuritySummit/ISG) for MS Office 2007 section 4.8, 4.9, 4.10 |
| Validate Template Name | There is a possibility that `w:attachedTemplate` refers to an invalid relationship.  Reference: ISG for MS Office 2007 section 4.5 |
| Remove Smart Tag | Smart Tags can executable code Reference: ISG for MS Office 2007 section 4.16 |
| Validate header or footer | Headers and footers are free-form text that can provide potential data disclosure threats.  Reference: ISG for Microsoft Office 2007 section 4.12 |
| Validate structured XML | Ensure syntactic and semantic validity |
| Validate zip structure | Office 2007 documents are zip files that contain various files and folders. Arbitrary data can be added into the central directory without authorization. Reference: ISG for Microsoft Office 2007 Section 3.1 to 3.6 |

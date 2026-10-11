<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/fixing--cellimages-xml-does-not-exist--error-in-xlsx-files--wps- -->

# Fixing 'cellimages.xml does not exist' Error in XLSX Files (WPS Office)

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [**Overview**](/docs/mdcore/knowledge-base/fixing--cellimages-xml-does-not-exist--error-in-xlsx-files--wps-#overview)

Some XLSX files created or edited with WPS Office fail in strict validators or CDR/sanitization pipelines with the error: “Invalid File Structure: Relationship file cellimages.xml does not exist.” This occurs when the package references xl/cellimages.xml but the file is missing.

## [**Symptoms**](/docs/mdcore/knowledge-base/fixing--cellimages-xml-does-not-exist--error-in-xlsx-files--wps-#symptoms)

- Security or sanitization tool logs: “Invalid File Structure: Relationship file cellimages.xml does not exist”
- File was saved with WPS Office, or shows WPS-specific content types/namespaces
- Excel may open the file normally or prompt to repair

## [**Why it happens**](/docs/mdcore/knowledge-base/fixing--cellimages-xml-does-not-exist--error-in-xlsx-files--wps-#why-it-happens)

XLSX is a ZIP of XML parts. Affected files declare and reference a cell image map but omit the actual part, creating a dangling reference.

> Typical signs inside the package:

- [Content_Types].xml contains an Override for /xl/cellimages.xml with a WPS content type
- xl/_rels/workbook.xml.rels contains a relationship of type http://www.wps.cn/officeDocument/2020/cellImage targeting cellimages.xml
- The physical file xl/cellimages.xml is absent

## [**Quick fix (recommended): Open in Excel and re-save**](/docs/mdcore/knowledge-base/fixing--cellimages-xml-does-not-exist--error-in-xlsx-files--wps-#quick-fix-recommended-open-in-excel-and-re-save)

1. Open the original XLSX in Microsoft Excel.
2. If prompted to repair, accept the repair.
3. File > Save As, and save a new copy (e.g., filename_fixed.xlsx).
4. Submit or use the newly saved file. Most workflows will now pass.

Why this works: Excel will remove or correct the dangling relationship so the package becomes structurally valid.

## [**Manual fix (advanced): Add a minimal xl/cellimages.xml**](/docs/mdcore/knowledge-base/fixing--cellimages-xml-does-not-exist--error-in-xlsx-files--wps-#manual-fix-advanced-add-a-minimal-xlcellimagesxml)

Use this if you cannot access Excel or need a deterministic repair for a single file.

1. Make a working copy of the XLSX file. Rename the copy from .xlsx to .zip.
2. Extract the ZIP. Navigate to the xl directory.
3. Create a new file named cellimages.xml inside xl with the minimal valid content below.
4. Repack: Select all extracted root items ([Content_Types].xml, _rels, docProps, xl, etc.), ZIP them (so these items are at ZIP root), then rename back to .xlsx.
5. Open the repaired file in Excel to verify no warnings; then submit it to your pipeline.

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<cellImages xmlns="http://www.wps.cn/officeDocument/2020/cellImage"></cellImages>

This minimal part satisfies the existing WPS Office relationship and content type without adding images or changing data.

## [**Verification**](/docs/mdcore/knowledge-base/fixing--cellimages-xml-does-not-exist--error-in-xlsx-files--wps-#verification)

1. Open the file in Microsoft Excel. Expect no repair prompts.
2. Run it through your CDR/sanitization or validation flow. The previous structural error should be gone.

## [**Prevention**](/docs/mdcore/knowledge-base/fixing--cellimages-xml-does-not-exist--error-in-xlsx-files--wps-#prevention)

- Prefer generating and final-saving XLSX files with Microsoft Excel or OOXML-compliant libraries when strict validation is required.
- If using WPS Office, update to the latest version and validate outputs in a staging environment before distribution.
- Avoid post-processing that removes parts from xl/ while leaving references in relationships or [Content_Types].xml.

## [**Troubleshooting / FAQ**](/docs/mdcore/knowledge-base/fixing--cellimages-xml-does-not-exist--error-in-xlsx-files--wps-#troubleshooting--faq)

Excel still shows a repair dialog after the fix

There may be additional structural issues (e.g., broken drawing or sharedStrings references). Repeat the inspect-and-repair process for any missing parts Excel mentions, or use Excel’s Save As to regenerate the package.

Can I just remove the relationship instead of adding cellimages.xml?

Yes, removing the dangling relationship and its content type entry can also resolve the error. However, ensure that no other parts depend on it. Adding a minimal part is often simpler and safer for WPS-linked cell images.

Is data altered by this fix?

No. The minimal cellimages.xml contains no images or data; it only restores structural consistency. Always keep a backup before editing.

How do I automate the repair?

Use a script that unzips the XLSX, checks for WPS cellImage references in [Content_Types].xml and xl/_rels/workbook.xml.rels, writes a minimal xl/cellimages.xml if missing, then re-zips. Libraries like Python zipfile + lxml, or .NET [System.IO](http://System.IO).Packaging/Open XML SDK can help.

If Further Assistance is required, please proceed to [log a support case or chat with our support engineer.](https://my.opswat.com/support)

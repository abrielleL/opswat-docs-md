<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/file-structure-validation/polyglot-detection -->

# Polyglot detection

A polyglot file is a single file that is validly interpreted as two or more different formats, for example an image that is also a Java archive, or a PDF carrying a complete ZIP after its logical end. Each face is standards-compliant on its own, so scanners that assign a file exactly one type analyze only that face and the other format rides through untouched.

Settings:

Full scan: Scan the entire file. When off, files larger than 16 MB are scanned only at their first and last 8 MB, trading depth for speed.

Example:

When `polyglot` is among the selected object types, each face is also carved out as its own file — `polyglot_part_1.pdf`, `polyglot_part_2.zip`, … and handed back to the workflow for full processing as what it really is.

Note: Only stacked-file polyglots are supported for now; other types of polyglots are coming soon.

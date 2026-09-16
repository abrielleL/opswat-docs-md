<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/file-structure-validation/what-is-file-structure-validation-engine- -->

# What is File Structure Validation engine?

File Structure Validation (FSV) is a module that inspects a file against its own format specification, enumerates every object the file contains, and blocks the file when its structure violate policy. FSV does not modify files. It returns a verdict and a detailed report; the original bytes are passed through unchanged or rejected outright.

FSV is built on the file-parsing technology behind Deep CDR, which gives it deep structural awareness across a wide range of formats — but it applies that awareness to a different decision: *is this file well-formed and permitted?* rather than *what must be removed from this file?*

### Supported formats (Total 166)

| **Family** | **File types** |
| --- | --- |
| Adobe | pdf, ai, ait |
| Microsoft Office Word | doc, docm, docx, dot, dotm, dotx, xml-docx |
| Microsoft Office Excel | xls, xlsb, xlsm, xlsx, xlt, xltm, xltx, xlam, xml-xls |
| Microsoft Office PowerPoint | ppt, pptm, pptx, pot, potm, potx, pps, ppsm, ppsx, ppam, sldm, sldx, xml-pptx |
| Visio | vdx, vsdm, vsdx, vssm, vssx, vstm, vstx, vsx, vtx |
| Microsoft Project | mpp |
| Microsoft PowerBI | pbix |
| OneNote | one |
| Open Document | odg, odp, ods, odt, otp, ots, ott |
| Hancom | cell, hwp, hwpx, hwt, show |
| Ichitaro | jhd, jtd, jtdc |
| DocuWorks (Windows only) | xdw, xbd, xct |
| RTF / Text | rtf, txt, log |
| Markup and data | bml, csv, har, hta, html, ics, jnlp, json, lyrx, mpd, rdf, tds, tsv, ttml, twb, vcf, vcs, xml, zei |
| Image | apng, bmp, cur, dcm, emf, emz, gif, heic, ico, jpg, jpx, mng, nef, png, svg, tga, tiff, tiff64, wdp, webp, wmf, wsq |
| Audio | aac, acm, aiff, bw64, bwf, mp3, ogg, opus, rf64, vtxt, w64, wav |
| Video | avi, flv, m2ts, m4a, mov, mp4, mpeg, mts, mxf, webm, wma, wmv |
| CAD and 3D | dwg, dwt, dws, dxf, dwf, dwfx, easm, jww, jwc, sfc, stp, p21, ifc, catpart, cgr, bfo, pxt, 3mf |
| Geospatial (ESRI / Shapefile) | shp, shx, prj, sbn, sbx, gdbtable, lpkx, mpkx |
| ML model | onnx, gguf, sts, parquet |
| Font | eot, otf, woff |
| Database | dbf |
| Email and contact | vcf, vcs, ics |
| Other | aem, dpa, lnk, url, nrbf, ribcd, crl |

Formats are added continuously, check the release notes of each version for newly supported types

<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/proactive-dlp/supported-metadata-type-in-pdlp -->

# Supported metadata type in PDLP

This page indicates the types of metadata supported by OPSWAT PDLP for each type of file. A list of these metadata can be found below:

|  | File Type | Metadata |
| --- | --- | --- |
| 1 | gif | XMP |
| 2 | tiff | XMP, EXIF |
| 3 | bmp | XMP |
| 4 | jpeg* | XMP, EXIF |
| 5 | png | XMP |
| 6 | pdf | built-in properties, custom properties |
| 7 | xls | built-in properties, custom properties |
| 8 | xlsx | built-in properties, custom properties |
| 9 | xlm | built-in properties, custom properties |
| 10 | xml_xls | built-in properties, custom properties |
| 11 | ppt | built-in properties, custom properties |
| 12 | pot | built-in properties, custom properties |
| 13 | pps | built-in properties, custom properties |
| 14 | pptx | built-in properties, custom properties |
| 15 | potx | built-in properties, custom properties |
| 16 | ppsx | built-in properties, custom properties |
| 17 | pptm | built-in properties, custom properties |
| 18 | potm | built-in properties, custom properties |
| 19 | ppsm | built-in properties, custom properties |
| 20 | rtf | built-in properties, custom properties |
| 21 | doc | built-in properties, custom properties |
| 22 | docx | built-in properties, custom properties |
| 23 | docm | built-in properties, custom properties |
| 24 | odt | built-in properties, custom properties |
| 25 | ods | built-in properties, custom properties |
| 26 | xml_doc | built-in properties, custom properties |
| 27 | xml_docx | built-in properties, custom properties |

The following list will provide a more detailed description of each of the metadata:

1. **XMP** (Extensible Metadata Platform): if available, except for the jpeg format, which requires some information to be retained in order to maintain the quality of the original image.
2. **EXIF** (Exchangeable Image File Format): if available, except for the jpeg format, which requires some information to be retained in order to maintain the quality of the original image.
3. **Built-in properties**: In cases where it is applicable; title, creator, subject, company, description manager, comment, producer, creationDate, modDat.
4. **Custom properties**: In cases where it is applicable; Extensible Metadata Platform such as the following: title, language, creators, contributors, rights, coverage, date, description, identifier, publisher, relation, source, subject, type, title, creator, lastModifiedBy, Company, revision, created, modified, codepage, author, keywords, comments, template, lastsaved by, *revisionnumber,* total edit_time, last_ printed, create_time, last_saved_time, num_pages, num_words, num_chars, thumbnail, creating_application, security, codepage_doc, category, presentation_target, bytes, lines, paragraphs, slides, notes, hidden_slides, mm_clips, scale_crop, heading_pairs, titles_of_parts, manager, company, links_dirty, chars_with_spaces, unused, shared_doc, link_base, hlinks, hlinks_changed, version, dig_sig, content_type, content_status, doc_version, and other fields that can be represented in xmp metadata (like user defined properties)

---

*In order to maintain the quality of the original image, some fields must be preserved. The following is a list of exceptions that are allowed for jpeg fields in metadata: quality, horizontal resolution, vertical resolution, resolution units, DPI info, bits per channel, CMYK color profile, color type, compression type, horizontal sampling, vertical sampling, palette, preblend alpha (if present), RGB color profile, sample rounding mode, color space, brightness value, contrast, compressed bpp, gain control, gamma, saturation, sharpness, orientation, white balance.

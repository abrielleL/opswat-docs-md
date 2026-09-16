<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/proactive-dlp/process-hidden-parts-in-a-cropped-image -->

# Process hidden parts in a cropped image

Cropping pictures inserted an Office file (such as a Word document, PowerPoint presentation, or Excel workbook) is a convenient tool in Microsoft Office apps that widely used by many people. The problem is that Office’s cropping tool only modifies how the cropped image is displayed in the body of the document. Actually, the original picture remains intact. Cropped portions of the image are not completely removed from the document and able to be seen by others. So, data leakage can occur if there is sensitive data in the trimmed areas.

Proactive DLP engine can detect sensitive data within cropped parts of images embedded in MS Word files (.doc and .docx) by leveraging Optical Character Recognition (OCR) technology. Furthermore, administrators also can configure this feature to permanently remove the cropped areas of the images.

**To configure this feature:**

- *Workflow Management > Workflows > Workflow name > Proactive DLP > Check for “Remove hidden part of embedded, cropped images”*

Support file types: MS Office (DOC/DOCX/XLS/XLSX/PPT/PPTX/PPS/PPSX/POT/POTX/PPTM/PPSM/POTM/Microsoft Office Word XML)

The feature is available from MetaDefender Core 4.19.2 or newer

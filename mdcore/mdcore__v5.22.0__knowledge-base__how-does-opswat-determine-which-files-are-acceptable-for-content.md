<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-does-opswat-determine-which-files-are-acceptable-for-content -->

# How Does OPSWAT Determine Which Files Are Acceptable for Content Disarm and Reconstruction (CDR)

Overview

Content Disarm and Reconstruction (CDR) is a proactive cybersecurity technology offered by OPSWAT that sanitizes files by removing potentially malicious elements while preserving usability. A critical part of this process is file acceptability determination — the mechanism that decides which files can be safely processed by CDR.

This article explains how OPSWAT determines whether a file is acceptable for CDR processing.

File Type Risk Assessment Criteria

✅ Is it a productivity file?

This can be debatable. While the file type may be intended for machine consumption rather than human reading, it could still be considered a “productive file” depending on the specific customer use case.

✅ Is there a public specification for this file type?

Yes — there appear to be public specifications or references available, which is a good indicator for potential support.

✅ Is this file type a proprietary format?

No — we couldn’t find any indication that this format is proprietary, which makes analysis and processing more feasible.

✅ Are there known attacks associated with this file type?

No known historical attacks have been found related to this format, which makes it less likely to be supported. However, if the customer has specific threat intelligence or incident data, we encourage them to share it with us for a more accurate assessment.

⚠️ Are there potential risk objects in this file type?

This is one of the key factors in determining whether CDR support is feasible. If a file format contains only static text and numerical data, without any interactive or executable components that typically introduce risk, CDR may offer limited benefit and might not be necessary.

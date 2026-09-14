<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/utilities-engines/difference-with-7zip -->

# Differences between OPSWAT Archive engine and 7-zip

7-Zip is a widely-used utility for archive file extraction, renowned for its SDK-ready capabilities, extensive support for various file formats, and open-source architecture. This makes it a favored option for developers seeking to incorporate robust extraction functionality into their applications. For example, OPSWAT integrates 7-Zip into its Archive Engine to facilitate efficient archive extraction. However, there are notable differences between the OPSWAT Archive Engine and 7-Zip:

- The OPSWAT Archive Engine extends beyond 7-Zip by leveraging multiple tools—including other open-source and commercial solutions—to achieve broader file format coverage. For instance, the Archive Engine supports the extraction of ALZ files (an ESTsoft proprietary format), which 7-Zip does not handle.
- OPSWAT's parsers are designed to process "container" file types, which are not conventional archive files such as MSG, EML, and PST. These file types can encapsulate other files within them (e.g., a PST file may contain multiple emails and contact files, while an MSG email file can include attachments). This capability ensures comprehensive extraction and analysis functionalities.
- 7-Zip is primarily designed for business extraction use cases and does not effectively address security scenarios where attackers attempt to deeply conceal data. Handling concatenated zip is an example, the 7-Zip extracts the first zip only, the OPSWAT Archive Engine can fully extract in this case.

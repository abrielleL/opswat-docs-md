<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-exclude--txt-files-from-the-file-type-engine- -->

# How to exclude .txt files from the File Type Engine?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Overview

To optimize processing time for large flat files (such as .txt or .csv), you may want to prevent the File Type Engine from analyzing these file types. This can significantly reduce total processing overhead, especially in high-volume environments.

This guide explains how to exclude large (10–20 GB size) .txt files by configuring the engine to detect only specific file types.

Use Case

- Large .txt / .csv files are causing increased processing time
- File type detection is not necessary for these formats
- You want to keep File Type Engine enabled for other file types

Solution

Instead of disabling the File Type Engine entirely, configure it to detect only specific file types, effectively excluding .txt.

This is done using the “Detect specific file types only” feature.

Configuration Steps

1. Access your MetaDefender Core configuration.
2. Locate the File Type Engine settings.
3. Enable the option:

- Detect specific file types only

4. Define the list of file types you want the engine to process:

- Include all required formats (e.g., pdf, docx, exe, etc.)
- Do NOT include txt (or csv if also excluding)

5. Save and apply the configuration.

Example

If you configure detection for:

pdf, docx, xlsx, exe

Then:

- ✅ These file types will be analyzed by the File Type Engine
- ❌ .txt files will be skipped by this engine

Expected Result

- Reduced processing time for large .txt / .csv files
- File Type Engine continues to operate for relevant formats
- Improved overall system performance in file-heavy workflows

Additional Notes

- This does not block or reject .txt files — it only skips File Type Engine processing for them
- Ensure other engines or policies still meet your security requirements
- Monitor performance after the change to validate improvement

Support: 

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

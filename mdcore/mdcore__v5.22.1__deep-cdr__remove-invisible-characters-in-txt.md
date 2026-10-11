<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/deep-cdr/remove-invisible-characters-in-txt -->

# Remove invisible characters in TXT

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Characters like **zero-width spaces (ZWSP)**, **soft hyphens**, or **bidirectional control characters** can be inserted into text without being visible to humans but still interpreted by machines. This method can be exploited in AI prompts to inject hidden instructions, manipulate outputs, or bypass security filters.

Deep CDR can efficiently detect and neutralize such attacks by cleansing the input and ensuring only legitimate content is processed.

Workflow > Deep CDR > Advanced Configurations > File type handling > Others > TXT.

Choose the **Preferred Encodings** is **UTF-8**. Enable **Remove Invisible Text**.

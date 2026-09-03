<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/why-do-i-receive--localization-file-has-xxx-keys-but-your-transl -->

# Why do I receive "localization file has XXX keys but your translated json has XXX keys"?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article is applied to MetaDefender Managed File Transfer releases deployed on Windows systems.

## [**Issue:**](/docs/mdmft/knowledge-base/why-do-i-receive--localization-file-has-xxx-keys-but-your-transl#issue)

An issue that may occur during the upload of translated JSON language files in MetaDefender Managed File Transfer is the presence of **duplicate keys**, which leads to a **conflict or key count mismatch error**. This can prevent the file from being accepted and the translations from being applied correctly.

## [**Solution:**](/docs/mdmft/knowledge-base/why-do-i-receive--localization-file-has-xxx-keys-but-your-transl#solution)

To resolve this issue:

1. **Review the translation file** Open the translated JSON file in a code or text editor with JSON validation (e.g., VS Code, Sublime Text, Notepad++ ).
2. **Identify and remove duplicate keys** Ensure that **each key is defined only once in the entire file**. Search for repeated keys and delete the redundant entries.
3. **Validate the JSON structure** After editing, use a JSON linter or validator tool to confirm the file is well-formed and contains no syntax errors.
4. **Re-upload the translation file** Submit the corrected file through the product’s language management interface.
5. **Change the user language setting** To apply and view the new translations, update the language setting for the user account. For guidance, refer to: [opswat.com/docs/mdmft/configuration/language](https://www.opswat.com/docs/mdmft/configuration/language)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

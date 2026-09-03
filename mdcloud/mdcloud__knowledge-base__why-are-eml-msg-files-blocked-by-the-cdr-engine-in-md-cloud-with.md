<!-- source: https://www.opswat.com/docs/mdcloud/knowledge-base/why-are-eml-msg-files-blocked-by-the-cdr-engine-in-md-cloud-with -->

# Why Are EML/MSG Files Blocked by the CDR Engine in MD Cloud with an “Unsupported File Type” Error?

**Issue**

When submitting .eml or .msg files to MD Cloud, the files may be blocked by the CDR engine with the following error: **Unsupported file type**

**Cause**

The Deep CDR engine does not directly support EML/MSG files as standalone file types. Without additional configuration, the CDR engine cannot extract or process the contents of the email container, which results in the file being blocked as an unsupported type.

**Resolution**

To allow the CDR engine to successfully process EML/MSG files you will need to enable the Unarchive option as well:

1. From the MD Cloud UI:

2. The required behavior can also be controlled via the API rule header. The required value for the rule header is:

- unarchive (performs both unarchiving and multiscanning)

**Summary**

- EML/MSG files are blocked because they are not directly supported by the Deep CDR engine
- These files must be unarchived so their contents can be scanned and sanitized
- Enabling the Unarchive option resolves the “Unsupported file type” error when submitting to MD Cloud

Support: 

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

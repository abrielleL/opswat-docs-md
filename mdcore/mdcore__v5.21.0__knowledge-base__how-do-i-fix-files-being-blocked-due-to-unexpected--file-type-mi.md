<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-do-i-fix-files-being-blocked-due-to-unexpected--file-type-mi -->

# How do I fix files being blocked due to unexpected "File type mismatch" verdict?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

#### [**Behavior**](/docs/mdcore/v5.21.0/knowledge-base/how-do-i-fix-files-being-blocked-due-to-unexpected--file-type-mi#behavior)

When File type engine's "Detect file type mismatch" option is enabled in your workflow, you may experience some files (such as JavaScript, Project Object Model) being blocked by File type engine due to "File Type Spoofing detected".

- Example 1: JavaScript source file being detected as TXT (plaintext) and blocked

- Example 2: Project Object Model file being detected as XML and blocked

- Example 3: JPEG File Interchange Format image (JFIF) being detected as JPG and blocked

In these examples, the underlying file type used by JavaScript, POM, JFIF files are plain text, XML, and JPEG respectively, even though their names have the extensions .js, .pom, and .jfif. Thus, that’s the type detected by File type engine.

#### [Remediation](/docs/mdcore/v5.21.0/knowledge-base/how-do-i-fix-files-being-blocked-due-to-unexpected--file-type-mi#remediation)

To avoid blocked verdict due to File type mismatch, there are 2 configurations you can use.

1. Add the filename's extension to the list of accepted extensions for that file type:

   - **Note :** more details can be found on the article on [Customize mismatch detection settings](/docs/mdcore/v5.21.0/knowledge-base/can-metadefender-core-block-renamed-files--such-as-renamed--exe-#customize-mismatch-detection-settings).
   - In workflow settings, go to “File Type”, and add the following in “Accepted extensions”:
   - File type ID: the file type detected by the engine (e.g. TXT, XML, JPG)
   - Extensions: the extension in the file’s name that you want to allow (e.g. js, pom, jfif):

- After making this configuration, the JavaScript source file is still detected as TXT, but it is no longer blocked due to mismatch:

2. In the case of text files, enable File type engine's machine-learning module to classify the file type based on its contents:

   - More details about this feature can be found at [Text detection with AI](/docs/mdcore/v5.21.0/utilities-engines/text-detection-with-ai-enhancement).
   - In Inventory > Modules > File Type, check 'Enable Machine learning module".
   - In workflow settings, go to "File Type" and enable "Classify with Machine Learning".
   - File type engine is now able to detect that the source file is JavaScript, and no longer blocked due to mismatch:

Warning:

The machine learning text detection feature is disabled by default, and unlike file signature matching, AI-based relies on heuristics and is not guaranteed to be precise.

In cases where the machine-learning feature isn’t able to correctly detect the file type of text files, **it’s generally preferred to use option 1 to customize the mismatch detection setting**.

Support:

If you have followed the instructions above but are still unable to fix source code files being blocked due to "File type mismatch", please follow these instructions on [**How to Create Support Package With Bundle Tools?**](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [**creating a support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

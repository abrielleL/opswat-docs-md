<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/why-are-my-script-files-being-detected-as-ascii-txt- -->

# Why are my script files being detected as ASCII TXT?

This article applies to all MetaDefender Kiosk V4 releases deployed on Windows systems.

### [**Overview:**](/docs/mdcore/v5.21.0/knowledge-base/why-are-my-script-files-being-detected-as-ascii-txt-#overview)

### [The FileType engine supports detection of common script file types such as BASH, JavaScript (JS), PowerShell (PS1), and Python (PY). However, due to the textual nature of these files, they may occasionally be identified as generic ASCII TXT files.](/docs/mdcore/v5.21.0/knowledge-base/why-are-my-script-files-being-detected-as-ascii-txt-#the-filetype-engine-supports-detection-of-common-script-file-types-such-as-bash-javascript-js-powershell-ps1-and-python-py-however-due-to-the-textual-nature-of-these-files-they-may-occasionally-be-identified-as-generic-ascii-txt-files)

**Why Misclassification Occurs:** Script files are fundamentally plain text and often lack unique signatures or structural characteristics that distinguish them from general text files. This makes accurate identification inherently difficult using conventional detection methods.

**Enhancing Detection with Machine Learning:** To improve detection accuracy for script files:

1. **Enable the Machine Learning module** in the FileType engine settings.
2. **Update your workflow** according to the steps outlined here: [Text detection with AI](/docs/mdcore/v5.21.0/utilities-engines/text-detection-with-ai-enhancement)

**Limitations and Expectations:** Even with advanced machine learning models, perfect detection is not guaranteed. Due to the flexible and diverse nature of script files:

- Some script files may still be misclassified.
- False positives and false negatives are possible and expected.

**Continuous Improvement and User Contribution:** Our team actively refines the AI models to improve accuracy. If you encounter misclassifications:

- Collect the misidentified samples.
- [Open a support case](https://my.opswat.com/support) with our team and attach the collected samples.

This feedback helps us fine-tune the models for better alignment with real-world use cases.

**Conclusion:** While detection of script files can be challenging, enabling AI enhancements and collaborating with support can significantly improve accuracy over time.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).

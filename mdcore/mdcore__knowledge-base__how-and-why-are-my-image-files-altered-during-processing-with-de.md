<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-and-why-are-my-image-files-altered-during-processing-with-de -->

# How and why are my image files altered during processing with Deep CDR and Proactive DLP?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

Pro-Tip:

● **MetaDefender Core’s Deep CDR** removes potential embedded threats by assuming all files to be malicious, then sanitizing and rebuilding files to ensure full and safe usability.

The Deep Content Disarm and Reconstruction process will ensure files are free from known and unknown threats, complex and sandbox aware threats, and threats equipped with malware evasion technology.

● **MetaDefender Core’s Proactive DLP** prevents potential data breaches and regulatory compliance violations by blocking sensitive and confidential data that may be included in files and emails.

The Data Loss Prevention process will ensure that all files, such as Microsoft Office and PDF docs, are free from sensitive details such as credit card and social security numbers.

**To process image files, the Deep CDR engine engages the following process:**

1. The image file is decompressed in order to access and process the raw data.
2. The engine then reconstructs a safe-to-use file by processing the pixels from the image.
3. During content disarming and reconstruction, potential steganography (data concealment) is treated by adding noisy data to ‘break’ hidden elements, while unnecessary data is discarded.
4. In the final stage of reconstruction, the file is compressed with the same image encoding as the original file.

**To process image files, the Proactive DLP engine engages the following process:**

1. The image file is decompressed in order to access and process the raw data.
2. The decompressed file is systematically scanned for sensitive and possibly confidential information.
3. This information, if any, is redacted or removed.
4. In the final stage of reconstruction, the file is compressed with the same image encoding as the original file.

Please Note:

Although the encoding (at Step 4) is the same, the image compression method may differ from the original method used.

As a result, the size of the graphics file will be altered - but the image quality will be largely retained.

MetaDefender Core guarantees a minimum of 99% image quality retention following processing with either Deep CDR or Proactive DLP.

Please Note:

If you encounter cases that file size changes compare to the original file size, these are the common reasons

1. The document contains images, and as mentioned earlier, the image file size can be changed, leading to the whole document file change
2. Some markup formats may get increased in size due to format decoration changing, e.g., spaces, tabs, or newlines added
Support:

If you believe your **Image Files Are Being Compromised During Deep CDR or Proactive DLP Processing**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).

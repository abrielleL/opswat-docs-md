<!-- source: https://www.opswat.com/docs/my/support-services/understand-what-you-are-reporting -->

# Understand What You’re Reporting

Understanding what you are reporting is important to ensure you provide the necessary information and context, which helps analysts evaluate each case more effectively.

Submission types are classified as either **false positives** or **false negatives**. For more information, see the [definition of a False Detection](https://www.opswat.com/docs/my/support-services/report-false-detection#definition-of-a-false-detection).

For a **false negative** request, there is nothing special to consider — simply complete the submission form following the instructions provided in the form, and an analyst will review the file to create the appropriate detection logic.

For a **false positive** request, multiple underlying sources may be involved. Within OPSWAT solutions, false positives typically originate from three components: multi scanning (MetaScan), file reputation, or sandbox. Understanding these sources is not necessary, but it helps users provide more accurate submission information, enabling analysts to process cases more efficiently.

- **MetaScan**: OPSWAT Multiscanning analyzes files with 30+ anti-malware engines to maximize detection rates. Learn more about this technology [here](https://www.opswat.com/technologies/multiscanning).
  - False positive example: AV vendor incorrectly flags a benign file as malicious.![](https://uploads.developerhub.io/prod/JYvy/agfbjbdmcmwvp125c78ntsdbkblxbdxaz7iuyiy3z45o4fpd44rbw73xgiif1cy9.png)

![](https://uploads.developerhub.io/prod/JYvy/t7qz7yic3i7xrhse0epjpdgz9qbfhisw1lqjuhi9ybqvr143149phej92zsfv562.png)

- **File Reputation**: The reputation engine classifies files as *known good*, *known bad*, or *unknown* by comparing hashes against a database of trusted and malicious files.
  - False positive example: the reputation engine incorrectly flags a benign file as known bad.![](https://uploads.developerhub.io/prod/JYvy/vumzw2kd01co72vy0trftzua0ostku3bahal4tsuitiumfwpt3j6cr3zbrrbdjsw.png)
- **Sandbox**: MetaDefender Sandbox detonates and analyzes files in a controlled environment, extracting IOCs and performing dynamic analysis to identify threats. Learn more about this technology [here](https://www.opswat.com/products/metadefender/sandbox).
  - False positive example: the sandbox incorrectly classifies a benign file as likely malicious or malicious.![](https://uploads.developerhub.io/prod/JYvy/vr0tflkoldlvxmh85crebin79z04tgbmt5cllj0z3cbx6074tb8w3am6nqa93ggs.png)

These three components are the primary sources of false positives. For each source, the submission form may request slightly different inputs to ensure analysts receive the right context. If users misidentify the source of the false detection, it is not a problem — analysts can determine the actual source from the exported scan results. To learn how to export results, check [How to Export Scan Results for Submission](https://www.opswat.com/docs/my/support-services/how-to-export-scan-results-for-submission).

> **Info**
>
> A false positive may sometimes be caused by more than one source (for example, both multiscanning and sandbox). If this happens, do not worry — simply select one option in the submission form. The analyst will identify all contributing sources from the scan results and ensure the false positive is addressed across them

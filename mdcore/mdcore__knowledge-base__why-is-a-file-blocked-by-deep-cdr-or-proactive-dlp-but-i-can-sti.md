<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-is-a-file-blocked-by-deep-cdr-or-proactive-dlp-but-i-can-sti -->

# Why is a file blocked by Deep CDR or Proactive DLP but I can still download the sanitized version?

This applies to MetaDefender Core version 5.13.1 and newer.

In many use cases, Deep CDR and Proactive DLP will mark files as blocked due to the detection of sensitive information as configured in the workflow. However, sanitized versions of these files will still be generated and will be available for retrieval as per the sanitized file availability configuration under the data retention policy.

This is expected behavior, as we intend to offer a rich customization experience so that the workflows can be tailored to each specific use case.

To ensure that if Deep CDR or Proactive DLP blocks a file it will not be available to be retrieved even if sanitized, we have introduced a new setting under the workflow configuration, in the General tab:

This setting will cause the download functionality for any files that are blocked by Deep CDR or Proactive DLP to be completely inaccessible, even if accessing these files in the MetaDefender Core UI.

In addition, we have introduced two more settings for improving scanning time, so that you can configure Deep CDR or Proactive DLP to not even attempt to process files if they are blocked by any other engines that run first, such as the AV engines.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).

<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-metadefender-core-blocks-sandbox-verdicts-that-are-not-marke -->

# Why MetaDefender Core blocks Sandbox Verdicts that are not marked to be blocked?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

By default, Sandbox Module for MetaDefender Core allows customizing the verdicts for which a scan should be marked as blocked:

However, it is very important to note that the following option under **Workflow** > **General** Tab will directly override the verdicts to be classified as Allowed, once activated:

## [What does that mean?](/docs/mdcore/knowledge-base/why-metadefender-core-blocks-sandbox-verdicts-that-are-not-marke#what-does-that-mean)

For instance, if Suspicious verdict is not marked to be blocked by Sandbox under the Engine Tab, but the **Processing results to be classified as Allowed** option is active without the **Suspicious Verdict by Sandbox** in the list of options, any Suspicious Verdict raised by Sandbox will directly be blocked, regardless of the individual engine blocking classifications.

*This is a security-first enhancement prioritized over the user experience with the main purpose of preventing accidental misconfigurations.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

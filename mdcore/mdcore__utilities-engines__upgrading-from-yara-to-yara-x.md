<!-- source: https://www.opswat.com/docs/mdcore/utilities-engines/upgrading-from-yara-to-yara-x -->

# Upgrading from YARA to YARA-X

## [Differences between YARA and YARA-X](/docs/mdcore/utilities-engines/upgrading-from-yara-to-yara-x#differences-between-yara-and-yara-x)

YARA-X introduces several changes and enhancements compared to traditional YARA. These differences can affect how rules are written, interpreted, and executed.

For a detailed comparison, refer to the official documentation: 🔗 [YARA-X vs YARA Rule Differences](https://virustotal.github.io/yara-x/docs/writing_rules/differences-with-yara/)

This resource outlines key distinctions in syntax, behavior, and supported features.

## [Mitigating issues](/docs/mdcore/utilities-engines/upgrading-from-yara-to-yara-x#mitigating-issues)

If there are any problems with the uploaded YARA rules, they will be indicated in the **Core UI**.

To investigate the issue further, you can:

- Check the **YARA engine log files** (accessible via the [**Logs**](https://www.opswat.com/docs/mdcore/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#enginelogs-folder) section).
- Use the [**YARA-X CLI tool**](https://virustotal.github.io/yara-x/) for detailed diagnostics.

#### [Resolution Steps](/docs/mdcore/utilities-engines/upgrading-from-yara-to-yara-x#resolution-steps)

1. **Fix the identified issues** in your YARA rules.
2. **Re-upload the corrected rules** to the system.
3. **Restart the engine** by disabling and then re-enabling it. This will trigger a new rule validation check.

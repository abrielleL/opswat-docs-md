<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/what-is-the-difference-between-the-archive-extraction-engine-v-s -->

# What is the difference between the Archive Extraction Engine V.S. Metascan Antivirus engines extraction?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

## [Description:](/docs/mdcore/v5.22.1/knowledge-base/what-is-the-difference-between-the-archive-extraction-engine-v-s#description)

The OPSWAT Archive Extraction engine works independently from the Metascan Antivirus engines.

## [Archive Extraction Engine](/docs/mdcore/v5.22.1/knowledge-base/what-is-the-difference-between-the-archive-extraction-engine-v-s#archive-extraction-engine)

**Location:**

Inventory > Modules > Utilities > Archive Extraction

**Functionality:**

- Supports more file types than individual Metascan Antivirus engine extractors.
- OPSWAT integrates 7-Zip into its Archive Engine to facilitate efficient archive extraction, for more details: [Differences between OPSWAT Archive engine and 7-zip](/docs/mdcore/v5.22.1/utilities-engines/difference-with-7zip)
- Generally faster than using individual Metascan Antivirus engine-based extractions.
- Recommended Archive Extraction method.
- Better performance and GUI visibility. Shows the complete recursive path and breakdown for extracted files.

- Configurable extraction limits that can be set globally for each file.

__ Example: __

## [Metascan Antivirus Engines](/docs/mdcore/v5.22.1/knowledge-base/what-is-the-difference-between-the-archive-extraction-engine-v-s#metascan-antivirus-engines)

**Location:**

Inventory > Modules > Metascan > click into individual engines

**Functionality:**

- Antivirus engines can extract files independently, this results in sequential processing, where the same archive may be extracted multiple times by different engines, this may lead to performance degradation.
- Best use if you are unable to enable the Archive Extraction Engine.
- Limited visibility, the GUI currently does not show the extracted files by each engine.
- Archive limits are set by the Antivirus vendor. Some contain configurable limits, whereas some do not have a setting.

**Examples:**

Ahnlab:

Avira:

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

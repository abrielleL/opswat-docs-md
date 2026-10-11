<!-- source: https://www.opswat.com/docs/filescan/3.2.0/faq/where-does-metadefender-sandbox-temporarily-stores-samples- -->

# Where does MetaDefender Sandbox temporarily stores samples?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article is applied to MetaDefender Sandbox releases deployed on Linux.

#### [**Question:**](/docs/filescan/3.2.0/faq/where-does-metadefender-sandbox-temporarily-stores-samples-#question)

Where does MetaDefender Sandbox temporarily store sample files during analysis?

#### [**Solution:**](/docs/filescan/3.2.0/faq/where-does-metadefender-sandbox-temporarily-stores-samples-#solution)

🔹 For version **2.0.0 and later**:

Submitted sample files are stored in the following directory:

`/home/sandbox/sandbox/webservice/src/storage/files`

🔹 For versions **prior to 2.0.0**:

`/home/filescanio/FileScanIO/webservice/src/storage/files`

#### [**Note:**](/docs/filescan/3.2.0/faq/where-does-metadefender-sandbox-temporarily-stores-samples-#note)

Ensure you have the appropriate permissions to access these directories. Modifying or deleting files during analysis may impact results or system stability.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

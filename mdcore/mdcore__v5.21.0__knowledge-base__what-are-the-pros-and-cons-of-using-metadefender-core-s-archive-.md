<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/what-are-the-pros-and-cons-of-using-metadefender-core-s-archive- -->

# What are the pros and cons of using MetaDefender Core's archive extraction engine vs. AV engine archive handling?

This article applies to all MetaDefender Core versions

> ### [MetaDefender Core Archive Extraction Engine](/docs/mdcore/v5.21.0/knowledge-base/what-are-the-pros-and-cons-of-using-metadefender-core-s-archive-#metadefender-core-archive-extraction-engine)

**Pros:**

- Provides detailed scan results for each file inside the archive in the scan report.
- Delivers more effective threat detection by leveraging multiple AV engines and additional modules (e.g., CDR, DLP) that can detect threats beyond the scope of traditional AV engines.
- Required if your MetaDefender Core deployment includes **CDR** or **DLP** and you want to apply these technologies to files within archives. (You can disregard this if your license does not include CDR or DLP.)
- Might be faster for large archives being scanned by many AV engines. However, it will depend on many other factors when it comes to performance.

**Cons:**

- May introduce noticeable processing overhead, especially when scanning small archives or using only a few AV engines. This can result in additional seconds of total processing time.

---

### [AV Engine Archive Handling](/docs/mdcore/v5.21.0/knowledge-base/what-are-the-pros-and-cons-of-using-metadefender-core-s-archive-#av-engine-archive-handling)

**Pros:**

- Can be faster for small archives, particularly when only a few AV engines (e.g., two) are enabled.

**Cons:**

- May become slower when scanning large archives with many AV engines, since each engine must extract and scan the same archive independently.
- Not all AV engines support archive handling, and OPSWAT does not maintain a list of which ones do.
- The range of supported archive formats may be narrower than that of MetaDefender Core’s archive extraction engine.
- Scan reports do not include per-file details for the contents of archives.

---

### [Recommendation](/docs/mdcore/v5.21.0/knowledge-base/what-are-the-pros-and-cons-of-using-metadefender-core-s-archive-#recommendation)

- **Use MetaDefender Core archive extraction** if you need detailed reporting, use CDR or DLP, or require the broadest file type coverage and most comprehensive threat detection.
- **Use AV engine archive handling** if your deployment is performance-sensitive, uses only a small number of AV engines, and does not rely on CDR or DLP.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

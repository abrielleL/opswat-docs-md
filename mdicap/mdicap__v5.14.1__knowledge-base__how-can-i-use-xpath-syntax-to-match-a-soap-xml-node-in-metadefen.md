<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/knowledge-base/how-can-i-use-xpath-syntax-to-match-a-soap-xml-node-in-metadefen -->

# How can I use XPath syntax to match a SOAP/XML node in MetaDefender ICAP Server?

This article applies to **MetaDefender ICAP Server** deployments on Windows and Linux, **version 5.11.0** and later.

## [Overview](/docs/mdicap/v5.14.1/knowledge-base/how-can-i-use-xpath-syntax-to-match-a-soap-xml-node-in-metadefen#overview)

Starting from **MetaDefender ICAP Server 5.11.0**, an **XPath-based node matching** option is available for SOAP/XML extraction. It enables the ICAP Server to locate and extract nodes by **name only**, without needing the full XML node path.

## [Standard Path Matching](/docs/mdicap/v5.14.1/knowledge-base/how-can-i-use-xpath-syntax-to-match-a-soap-xml-node-in-metadefen#standard-path-matching)

Before version 5.11.0, ICAP Server required the **exact XML path** to locate nodes in SOAP/XML messages.

For example, with the XML below:

XmlCopy<?xml version="1.0" encoding="UTF-8"?>
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
<s:Body>
<processBatch xmlns="http://example.com/batch/v1">
<BatchHeader>
<BatchID xmlns="">BATCH-DEMO-003</BatchID>
<Timestamp xmlns="">2025-10-27T14:10:00Z</Timestamp>
<Source xmlns="">DemoSystem</Source>
</BatchHeader>
<BatchItems>
<Item>
<ItemID xmlns="">ITEM-A01</ItemID>
<Document>
<Filename xmlns="">doc1.txt</Filename>
<Content>
<Data xmlns="">U2hvcnQgZGVtbyBjb250ZW50Lg==</Data>
</Content>
</Document>
</Item>
<Item>
<ItemID xmlns="">ITEM-EICAR</ItemID>
<Document>
<Filename xmlns="">test_eicar.com</Filename>
<Content>
<Data xmlns="">WDVPIVAlQEFQWzRcUFpYNTQoUF4pN0NDKTd9JEVJQ0FSLVNUQU5EQVJELUFOVElWSVJVUy1URVNULUZJTEUhJEgrSCo=</Data>
</Content>
</Document>
</Item>
</BatchItems>
</processBatch>
</s:Body>
</s:Envelope>

To match the Base64 data content, users needed to configure the full node path as below:

doc1.txt:
//s:Envelope/s:Body/processBatch/BatchItems/Item[1]/Document/Content/Data
----
test_eicar.com:
//s:Envelope/s:Body/processBatch/BatchItems/Item[2]/Document/Content/Data
## [XPath Matching](/docs/mdicap/v5.14.1/knowledge-base/how-can-i-use-xpath-syntax-to-match-a-soap-xml-node-in-metadefen#xpath-matching)

From version **5.11.0**, ICAP Server adds support for **XPath-based node matching**,which allows node selection regardless of depth or namespace.

Example:

- **Query type:** XPath
- **Node selector:** `//Data`

With this, ICAP Server automatically matches any `<Data>` node appearing in the XML structure.

The Base64 data or attachments can then be sent to **MetaDefender Core** for scanning, further enhancing the ICAP and Core capabilities to detect and prevent malicious content. In the sample XML path, this allows the system to identify and block the **EICAR test file** contained within the XML structure.

## [Known Limitations](/docs/mdicap/v5.14.1/knowledge-base/how-can-i-use-xpath-syntax-to-match-a-soap-xml-node-in-metadefen#known-limitations)

- XPath Node Matching is supported **only for SOAP/XML extraction**.
- Only the `//` XPath syntax is supported. Other syntax types such as `..` or `@` are **not supported**.
- ICAP can extract nodes **only if they do not contain nested nodes**.

  - With the above XML as example:

    - If the selector is `//Data`, ICAP can extract the node content.
    - If the selector is `//Content` (which contains the `Data` node), ICAP cannot extract the content.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

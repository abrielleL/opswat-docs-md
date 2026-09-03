<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/deep-cdr/allow-hyperlinks -->

# Allow Hyperlinks

Despite hyperlinks’ centrality to the user experience, connecting pages and sites with a single click, they could be a high-risk attack vector. To ensure that all potential threats in files were eliminated before reaching the users, hyperlinks should be removed during Deep CDR process by default. However, we understand that usable hyperlinks are essential and important for some businesses. Thus, we introduce a flexible configuration enabling administrators to allow hyperlinks or domains that they deem safe.

***Workflow Management > Workflows > Workflow name > Enable Allowlist Hyperlink***

**Allowlist Pattern:**

- Regular expression
- or **filepath**:<file path to a file which contains a regular expression list, line by line>, e.g.,

The above example allows all links from **opswat.com** domain/sub domain.

An example output when processing a file with two hyperlinks (<http://malicious.com>, <https://docs.opswat.com/mdcore/deep-cdr>) on it.

Supported file types: MS Office, HTML, Calendar

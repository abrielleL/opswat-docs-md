<!-- source: https://www.opswat.com/docs/mdcloud/compliance/tenant-isolation-policy -->

# Tenant Isolation Policy

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
### [**How MetaDefender Cloud keeps your data separate from other customers**](/docs/mdcloud/compliance/tenant-isolation-policy#how-metadefender-cloud-keeps-your-data-separate-from-other-customers)

MetaDefender Cloud is a shared service: all customers use the same databases, storage and scanning infrastructure. Your data is kept apart from other customers' data by access checks on every request, at each of the layers below.

| Statement to the customer |
| --- |
| **Your API keys.** Every request to MetaDefender Cloud is tied to you through the API key that makes it: to your organisation, or, if you use MetaDefender Cloud as a standalone user, to your account. Results of scans made with private processing, your sanitized files, your scan history and your organisation settings can be reached only with an API key of your organisation or account. Results of scans made without private processing are part of MetaDefender Cloud's shared threat intelligence and can be looked up by other users by file hash. Use private processing for files whose results must not be visible to others. |
| **Your organisation and sub-organisations.** If you split your account into sub-organisations, each one sees only its own data and the data of the sub-organizations below it, offering a top-down view. A parent organisation can see the data of its sub-organisations, including private results. A sub-organisation cannot read the data of its parent organisation or of another sub-organisation. |
| **Your private results.** When you use private processing, your results, your sanitized files and your scan history are visible only to your organisation and the organisations above it, or only to you if you use MetaDefender Cloud as a standalone user. They are not shown to other users of MetaDefender Cloud and are processed only by OPSWAT and the sub-processors listed in OPSWAT's sub-processor list. |
| **How your files are processed.** Files are scanned on shared processing infrastructure. Each scan is tracked by its own request and file identifiers, and its results are returned only to the MetaDefender Cloud service that submitted it. Access to results is checked by MetaDefender Cloud before anything is returned to you. If you use private processing, the file you upload is deleted once the scan is complete. Files uploaded without private processing are kept as described in [**Customer Data Offloading Policy**](/docs/mdcloud/compliance/customer-data-offloading-policy). |
| **Separate environments.** The production service that handles your data runs separately from the environments OPSWAT uses for development and testing. |
| **How this is checked.** OPSWAT runs automated tests on every release of the service to confirm that one customer cannot reach another customer's data. |

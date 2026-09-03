<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/configuration/metadefender-core-specific-inventory-properties -->

# MetaDefender Core specific inventory properties

## [Query parameters](/docs/mdicap/v5.14.1/configuration/metadefender-core-specific-inventory-properties#query-parameters)

Addresses specified in CORE URI ADDRESS may contain optional query parameters for specific use cases.

## [Syntax](/docs/mdicap/v5.14.1/configuration/metadefender-core-specific-inventory-properties#syntax)

With the optional query parameters the Core URI is formatted as follows:

URI schema with query parameter
scheme://host:port[?query]
## [Valid parameters](/docs/mdicap/v5.14.1/configuration/metadefender-core-specific-inventory-properties#valid-parameters)

| Name | Value | Use case | Example |
| --- | --- | --- | --- |
| apikey | 32 characters long API key of an account that belongs to the role the Core side rule is restricted to. | Core side rules may be restricted to roles (for details see [3.6.4. Workflow rule configuration](https://onlinehelp.opswat.com/corev4/3.6.4._Workflow_rule_configuration.html) in [MetaDefender Core v4 documentation](https://onlinehelp.opswat.com/corev4/)). Email Security can use these rules if:   1. A user is created on Core,     1. That belongs to the role the Core side rule is restricted to;    2. And the user has an API key generated. 2. In Email Security the Core is added to a server profile     1. And the API key above is specified in the Core URI. | URI example with query parameter `https://127.0.0.1:8058?apikey=24a586f3023b4309b65aa1974198d6c6` |

## [Workflow](/docs/mdicap/v5.14.1/configuration/metadefender-core-specific-inventory-properties#workflow)

Right after the CORE URI ADDRESS has been specified, and is valid (connection can be established) the WORKFLOW drop-down list is populated with the available workflow on the corresponding MetaDefender Core instance.

The desired workflow may be selected from the configured Core's available rules. Default is *Automatic*.

Note

Pleaf the security rules on the configured MetaDefender Core under **Policy > Security rules** are limited to a specific user agent other than mdicapserver or restricted to specific roles other than what is specified in the server URI, then those workflow will not be available in MetaDefender ICAP Server.

MetaDefender ICAP Server identifies itself on MetaDefender Core with the user agent mdicapserver.

<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/sso-integrations -->

# SSO Integrations

Summarize Page    Connect to Cursor Connect to VS Code

Some SSO providers deviate from standard RFC specifications. When integrating these providers with product_name, follow the specific instructions below to ensure compatibility:

| Product | Configuration |
| --- | --- |
| **ManageEngine ADSelfService Plus** | PKCE Support does not support Proof Key for Code Exchange (PKCE) when using the Authorization Code Flow. Please **disable PKCE support** in product_name when configuring this integration. |
| **ManageEngine ADSelfService Plus** | Certain versions of ADSelfService Plus require **TLS 1.2**. To ensure compatibility, enable TLS 1.2 support in product_name by navigating to the Server Configuration tab. |

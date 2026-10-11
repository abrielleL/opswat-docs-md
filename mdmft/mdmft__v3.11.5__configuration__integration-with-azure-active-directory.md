<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/configuration/integration-with-azure-active-directory -->

# Integration with Azure Active Directory

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

MetaDefender Managed File Transfer interacts with Active Directory via the LDAP(S) protocol. Configure the cloud domain to allow this exchange.

If not already configured, follow these steps:

1. [Create a managed domain](https://docs.microsoft.com/en-us/azure/active-directory-domain-services/tutorial-create-instance)
2. [Configure the virtual network](https://docs.microsoft.com/en-us/azure/active-directory-domain-services/tutorial-configure-networking)
3. [Configure secure LDAP](https://docs.microsoft.com/en-us/azure/active-directory-domain-services/tutorial-configure-ldaps) *Note: A certificate issued by a certified certificate authority is required.*

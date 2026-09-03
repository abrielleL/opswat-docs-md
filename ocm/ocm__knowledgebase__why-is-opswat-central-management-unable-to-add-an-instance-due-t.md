<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/why-is-opswat-central-management-unable-to-add-an-instance-due-t -->

# Why is OPSWAT Central Management unable to add an instance due to domain name restrictions?

After enabling HTTPS for OPSWAT products with underscore in a domain name, OPSWAT Central Management returns “Could not reach the server”.

If the OCM UI displays the error message **"Could not reach the server"** and the domain name contains an underscore (`_`), it means that OCM does not support domain names with underscores.

This is because OCM uses a library to validate domain names according to the **DNS standard** — which only permits:

- **Letters** (a-z)
- **Numbers** (0-9)
- **Hyphens** (-)

While modern web browsers may allow URLs with underscores in domain names, the validation library used by OCM strictly follows DNS specifications, resulting in an error if an underscore is detected.

To resolve this issue, ensure the domain name follows standard DNS naming rules, avoiding the use of underscores.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

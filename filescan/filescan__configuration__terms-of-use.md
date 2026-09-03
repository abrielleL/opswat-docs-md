<!-- source: https://www.opswat.com/docs/filescan/configuration/terms-of-use -->

# Terms of Use

These are the identifiers / keys related to a service's terms of use, privacy policy, cookie policy, and other legal documents.

The location of the ***Terms of Use*** is **Admin Panel > Settings >** [**Configuration**](https://www.filescan.io/admin/settings/config)**> Terms of Use .**

Screenshot of Configuration page of MetaDefender Sandbox

| Field | Description |
| --- | --- |
| `TERMLY_ACCOUNT_ID` | Identifier for the account or entity associated with the terms of use. |
| `TERMLY_PRIVACY_POLICY_ID` | Unique identifier for the privacy policy of the service. |
| `TERMLY_TERMS_ID` | Unique identifier for the terms of use document. |
| `TERMLY_COOKIE_POLICY_ID` | Unique identifier for the cookie policy of the service. |
| `TERMS_LOCAL_SOURCE` | A flag indicating to show the source or location of the terms of use. |
| `ASK_TERMS_CONSENT` | A flag indicating whether the service asks users to consent to the terms of use explicitly. Requesting users to consent happens per scan/upload. If it is deemed unnecessary, it is possible to turn it off here. |

Identifiers are used in the service's backend to reference specific legal documents or settings related to terms of use, privacy, and cookies.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

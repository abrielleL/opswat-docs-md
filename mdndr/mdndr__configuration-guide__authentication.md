<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/authentication -->

# Authentication

System setting (global). This setting applies to the whole system and to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → System settings → Authentication

Control how users sign in. Choose local accounts, single sign-on (SSO), or both. Set the local password policy and the SSO providers.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Auth Login Mode** | Login mode selector (local_only, local_plus_sso, sso_only). | `local_only` | `local_only`, `local_plus_sso`, `sso_only` | Restart needed |
| **Password Policy** | Local username/password complexity and rotation policy. Applies only to local accounts; SSO identities are unaffected. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Providers** | Configured OIDC/SAML providers. Enabling local_plus_sso or sso_only requires at least one enabled, valid provider. Capped at 16. This is a group of settings. See the sub-settings below. | — | list of groups | Restart needed |
| **Public Base Url** | Public base URL of the deployment (used to build SSO redirect/ACS URLs). | — | text | Restart needed |
| **Default Redirect Path** | Same-origin relative path to redirect to after a successful SSO login. Must start with a single '/'; absolute and protocol-relative URLs are rejected to prevent open redirects. | `/dashboard` | text; up to 512 characters | Restart needed |
| **Cookie** | SSO state-cookie settings. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |

#### [Authentication: PasswordPolicyConfig sub-settings](/docs/mdndr/configuration-guide/authentication#authentication-passwordpolicyconfig-sub-settings)

*Admin-configurable local-password complexity and rotation policy. on local user create / self password change / admin-triggered reset, and (for max_age_days) at login time. It applies only to local username/password accounts; SSO identities carry no local password and are unaffected.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Min Length** | Minimum password length. Capped at 72 to match the bcrypt byte limit. | `12` | number; 8 to 72 | — |
| **Require Uppercase** | Require at least one uppercase letter. | On | on/off | — |
| **Require Lowercase** | Require at least one lowercase letter. | On | on/off | — |
| **Require Digit** | Require at least one digit. | On | on/off | — |
| **Require Special** | Require at least one special (non-alphanumeric) character. | On | on/off | — |
| **Max Age Days** | Maximum password age in days before rotation is forced at login. 0 disables expiry (passwords never expire). | `0` | number; 0 to 3650; unit: days | — |
| **Prevent Reuse Count** | Number of previous passwords that may not be reused. 0 disables history checks. | `0` | number; 0 to 24 | — |

#### [Authentication: SSOProviderConfig sub-settings](/docs/mdndr/configuration-guide/authentication#authentication-ssoproviderconfig-sub-settings)

*A single external identity provider (oidc or saml). Common identity fields apply to both types. issuer_url/discovery_url/ client_id are OIDC-oriented; idp_metadata_*/sp_*/acs_url/ name_id_format are SAML-oriented. Unused fields for a given type are left at their defaults. Secret material (client_secret, sp_private_key) is modeled as pydantic.SecretStr following the ontology convention (see service_configs.py); SecretStr values are never serialized inline into the generated JSON schema. The public SP certificate is a non-secret string.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Key** | Stable provider key/slug (used in callback URLs and audit). | *(empty)* | text; up to 64 characters | — |
| **Display Name** | Human-readable provider name shown on the login page. | *(empty)* | text | — |
| **Type** | Provider protocol type (oidc or saml). | `oidc` | `oidc`, `saml` | — |
| **Enabled** | Whether this provider is active. | Off | on/off | — |
| **Issuer Url** | OIDC issuer URL (iss); used to validate ID tokens. | — | text | — |
| **Discovery Url** | OIDC discovery document URL (.well-known/openid-configuration). | — | text | — |
| **Client Id** | OIDC client ID registered with the provider. | — | text | — |
| **Client Secret** | OIDC client secret (secret; never serialized inline). | *(empty)* | text | Sensitive (hidden) |
| **Redirect Url** | OIDC redirect/callback URL registered with the provider. | — | text | — |
| **Scopes** | OIDC scopes to request. | `["openid", "profile", "email"]` | list of string | — |
| **Idp Metadata Url** | SAML IdP metadata URL. | — | text | — |
| **Idp Metadata File** | Path to a mounted SAML IdP metadata XML file (alternative to URL). | — | text | — |
| **Sp Entity Id** | SAML Service Provider entity ID. | — | text | — |
| **Acs Url** | SAML Assertion Consumer Service (ACS) URL. | — | text | — |
| **Name ID Format** | SAML NameID format. | `emailAddress` | `emailAddress`, `persistent`, `transient`, `unspecified` | — |
| **Sp Private Key** | SAML SP private key (secret; never serialized inline). | *(empty)* | text | Sensitive (hidden) |
| **Sp Certificate** | SAML SP public certificate (PEM; non-secret). | — | text | — |
| **Username Claim** | Claim/attribute mapped to the local username. | `preferred_username` | text | — |
| **Email Claim** | Claim/attribute mapped to the local email. | `email` | text | — |
| **Groups Claim** | Claim/attribute carrying the user's groups. | `groups` | text | — |
| **Roles Claim** | Claim/attribute carrying the user's roles. | — | text | — |
| **Allowed Domains** | Optional allow-list of email domains permitted to sign in. | — | list of string | — |
| **Allowed Tenants** | Optional allow-list of tenant IDs (e.g. Entra tenant) permitted to sign in. | — | list of string | — |
| **Require Idp Mfa** | Fail closed unless the IdP response satisfies MFA (amr/acr / AuthnContext). | Off | on/off | — |
| **Mfa Acr Values** | Required acr values / authentication methods when require_idp_mfa is set. | — | list of string | — |
| **Idp Initiated Enabled** | Allow IdP-initiated login (SAML). Off by default for security. | Off | on/off | — |
| **Slo Enabled** | Enable single logout (SLO) with this provider. | Off | on/off | — |
| **Jit Enabled** | Just-in-time provision local users on first successful login. | On | on/off | — |
| **Auto Link Enabled** | Automatically link SSO identities to existing local users by email. | Off | on/off | — |
| **Sync Roles** | Sync local roles from the provider's roles claim on each login. | Off | on/off | — |
| **Sync Scopes** | Sync local scopes/permissions from the provider on each login. | Off | on/off | — |
| **Group Mappings** | Ordered list of external IdP group/role -> local role/scope mappings, applied when sync_roles/sync_scopes is enabled. External values that match no mapping grant nothing (fail-closed), so the IdP can never inject an unmapped NDR role. Capped at 64. | — | list of groups | — |
| **Default Role** | Baseline local role granted to every user provisioned through this provider (JIT), independent of group mappings. Empty grants no baseline role. Group mappings can elevate above it (e.g. default 'user' with 'ndr-admins' -> 'admin'). | — | text | — |

#### [Authentication: SSOCookieConfig sub-settings](/docs/mdndr/configuration-guide/authentication#authentication-ssocookieconfig-sub-settings)

*Browser-binding state-cookie settings for the SSO login flow. Cookie attributes must be config-driven: OIDC top-level GET callbacks can use SameSite=Lax while SAML POST-binding ACS needs SameSite=None; Secure.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **State Cookie Name** | Name of the SSO state/browser-binding cookie. | `ndr_sso_state` | text | — |
| **Secure** | Set the Secure attribute on SSO state cookies (required in production). | On | on/off | — |
| **Same Site** | SameSite for OIDC state cookies (Lax works for top-level GET callbacks). | `lax` | `lax`, `strict`, `none` | — |
| **Saml Same Site** | SameSite for SAML state cookies (None+Secure required for cross-site POST ACS). | `none` | `lax`, `strict`, `none` | — |
| **State Ttl Seconds** | Time-to-live for a pending SSO login state before it expires. | `600` | number; 30 to 3600; unit: seconds | — |

**Related:** [Users, groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

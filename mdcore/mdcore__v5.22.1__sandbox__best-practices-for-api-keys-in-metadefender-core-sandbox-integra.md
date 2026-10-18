<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/sandbox/best-practices-for-api-keys-in-metadefender-core-sandbox-integra -->

# Best practices for API keys in MetaDefender Core Sandbox integrations

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Best practices for API keys in MetaDefender Core → Sandbox integrations (least privilege)

# [**Overview**](/docs/mdcore/v5.22.1/sandbox/best-practices-for-api-keys-in-metadefender-core-sandbox-integra#overview)

When MetaDefender Core integrates with a remote Sandbox, Core authenticates using a Sandbox API key. The API key inherits the permissions of the Sandbox user that owns it. Therefore, the owning user must have the minimal capabilities required to submit samples for detonation and read analysis results.

## [**Scope and applicability**](/docs/mdcore/v5.22.1/sandbox/best-practices-for-api-keys-in-metadefender-core-sandbox-integra#scope-and-applicability)

- Core submitting files or URLs to a Sandbox for detonation/analysis and retrieving verdicts and reports.
- Environments spanning dev, test, staging, and production where Core talks to one or more Sandbox tenants.

The API key itself does not hold permissions; it reflects the privileges of the Sandbox user. Adjust the user’s role to change effective permissions.

## [**Goal**](/docs/mdcore/v5.22.1/sandbox/best-practices-for-api-keys-in-metadefender-core-sandbox-integra#goal)

Enable MetaDefender Core to submit items to the Sandbox and retrieve results using a least-privilege, auditable service account model.

## [**Recommended account model (Sandbox side)**](/docs/mdcore/v5.22.1/sandbox/best-practices-for-api-keys-in-metadefender-core-sandbox-integra#recommended-account-model-sandbox-side)

- Create a dedicated integration user (service account), for example `svc_core_to_sandbox`.
- If supported, mark it as a service account to improve audit clarity. This label does not grant permissions; role assignment does.

## [**Minimum Sandbox permissions**](/docs/mdcore/v5.22.1/sandbox/best-practices-for-api-keys-in-metadefender-core-sandbox-integra#minimum-sandbox-permissions)

- Ability to upload/submit files or URLs for detonation.
- Ability to access/read analysis results and verdicts.

In many RBAC models, an Analyst-type or equivalent operational role covering “submission + results access” is sufficient. Avoid administrative roles unless required for tenant configuration, user management, or global policy changes.

Principle of least privilege: grant only submission and read-results scopes to reduce blast radius if the key is exposed.

## [**API key hygiene and security best practices**](/docs/mdcore/v5.22.1/sandbox/best-practices-for-api-keys-in-metadefender-core-sandbox-integra#api-key-hygiene-and-security-best-practices)

- Use a dedicated integration user, never a personal account.
- Scope access to the smallest organizational boundary needed (specific tenant, org, or project).
- Issue separate API keys per integration and per environment (dev/test/stage/prod) to isolate risk and simplify revocation.
- Store keys in a secure secret manager; never embed in source control, CI logs, or config files in plaintext.
- Minimize key exposure in telemetry: redact keys from logs, traces, and error messages.
- Rotate keys regularly and on personnel or role changes; automate rotation where possible.
- Constrain network paths so only the Core system can reach the Sandbox API (IP allowlists, private connectivity, or mTLS where available).

## [**Configuration guidance (high level)**](/docs/mdcore/v5.22.1/sandbox/best-practices-for-api-keys-in-metadefender-core-sandbox-integra#configuration-guidance-high-level)

1. Create the Sandbox service account `svc_core_to_sandbox` and assign the lowest role that still permits submissions and results access.
2. Generate an API key for that account; store it in your organization’s approved secret manager (for example, a vault) and reference it from Core’s configuration.
3. Restrict network egress/ingress to the Sandbox API endpoint from the Core host or cluster only; verify TLS and certificate pinning options if supported.
4. Validate end-to-end by submitting a benign sample and confirming retrieval of the corresponding analysis result.

## [**Operational checklist**](/docs/mdcore/v5.22.1/sandbox/best-practices-for-api-keys-in-metadefender-core-sandbox-integra#operational-checklist)

- Sandbox integration user created (`svc_core_to_sandbox`)
- User assigned the lowest role that still permits submit + results access
- API key stored in an approved secret manager and referenced by Core without plaintext exposure
- Key rotation cadence, ownership, and revocation procedure documented

## [**Common pitfalls to avoid**](/docs/mdcore/v5.22.1/sandbox/best-practices-for-api-keys-in-metadefender-core-sandbox-integra#common-pitfalls-to-avoid)

- Using admin or global roles for routine submissions, expanding attack surface unnecessarily.
- Reusing one API key across multiple environments or integrations, complicating audit and revocation.
- Leaving keys in application logs or build artifacts where they can be harvested.

# [Support](/docs/mdcore/v5.22.1/sandbox/best-practices-for-api-keys-in-metadefender-core-sandbox-integra#support)

If further assistance is required, please proceed to log a support case or chat with our support engineer.

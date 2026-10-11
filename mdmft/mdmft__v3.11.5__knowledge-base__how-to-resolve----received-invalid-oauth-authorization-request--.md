<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/how-to-resolve----received-invalid-oauth-authorization-request-- -->

# How to Resolve “Received Invalid OAuth Authorization Request” Error When Integrating MFT with ADFS via SAML

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool Check Your Version:

This article applies to all MetaDefender Managed File Transfer releases deployed on Windows.

This article addresses an issue encountered when integrating MetaDefender Managed File Transfer with ADFS using SAML authentication. The error message received during login was:

Info:

`Received invalid OAuth authorization request. The received 'redirect_uri' parameter is not a valid registered direct URI for the client identifier.`

The issue was caused by a mismatch between the '**redirect_uri**' configured in the MFT application and the one registered in the Identity Provider (**IdP**) settings in **ADFS**. The IdP was rejecting the OAuth request due to the unrecognized or incorrect redirect URI.

### [Resolution Steps](/docs/mdmft/v3.11.5/knowledge-base/how-to-resolve----received-invalid-oauth-authorization-request--#resolution-steps)

#### [Step 1: Verify 'redirect_uri' in MFT Configuration](/docs/mdmft/v3.11.5/knowledge-base/how-to-resolve----received-invalid-oauth-authorization-request--#step-1-verify-redirect_uri-in-mft-configuration)

- Access the MFT server configuration.
- Locate the SAML or OAuth configuration section where the 'redirect_uri' is specified.
- Make note of the exact URI value.

#### [Step 2: Verify Registered 'redirect_uri' in ADFS](/docs/mdmft/v3.11.5/knowledge-base/how-to-resolve----received-invalid-oauth-authorization-request--#step-2-verify-registered-redirect_uri-in-adfs)

- Log in to the ADFS management console.
- Navigate to the Relying Party Trusts or App Registrations, depending on your setup.
- Confirm that the 'redirect_uri' registered for the client application exactly matches the value from MFT.

#### [Step 3: Correct the URI if Mismatched](/docs/mdmft/v3.11.5/knowledge-base/how-to-resolve----received-invalid-oauth-authorization-request--#step-3-correct-the-uri-if-mismatched)

- If the URIs do not match:

  - Either update the MFT configuration to match the value in ADFS,
  - Or update the ADFS registered 'redirect_uri' to reflect the value used in MFT.

Warning:

The 'redirect_uri' is case-sensitive and must be an exact match, including trailing slashes and protocol (e.g., `https://`)

#### [Step 4: Test the Integration](/docs/mdmft/v3.11.5/knowledge-base/how-to-resolve----received-invalid-oauth-authorization-request--#step-4-test-the-integration)

- Restart the MFT service if needed.
- Attempt to log in via the ADFS SAML flow.
- Confirm that the login process completes without errors.

### [Note](/docs/mdmft/v3.11.5/knowledge-base/how-to-resolve----received-invalid-oauth-authorization-request--#note)

- If you are using a load balancer or proxy in front of MFT, ensure that the public-facing URL is the one registered as the **'redirect_uri'.**
- If multiple environments are in use (e.g., staging, production), ensure each environment has the appropriate **'redirect_uri'** registered.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

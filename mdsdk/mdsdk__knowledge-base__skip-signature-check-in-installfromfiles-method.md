<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method -->

# Understanding the skip_signature_check input in the InstallFromFiles method

## [Overview](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#overview)

The `skip_signature_check` option tells the SDK whether to **verify the digital signature of the installer file before executing it** when calling the `InstallFromFiles` method.

| **Field Name** | `skip_signature_check` |
| --- | --- |
| Data Type | Integer |
| Accepted Value | `0` or `1` |
| Default Value | `1` (signature verification is **skipped**) |
| Optional | Yes |
| Platforms | Windows and macOS (on Linux, package integrity is handled by the platform package manager, e.g., APT/dpkg) |

- `skip_signature_check = 1` (default): the SDK does **not** verify the installer's digital signature before running it.
- `skip_signature_check = 0`: the SDK verifies the installer's signature against the signing information stored in the OPSWAT patch data **before** the installer is executed. If any verification step fails, the installation does not run.
- Any value other than `0` or `1` is rejected with `WAAPI_ERROR_INVALID_INPUT_ARGS -20`.

## [What the SDK verifies when `skip_signature_check = 0`](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#what-the-sdk-verifies-when-skip_signature_check--0)

The verification runs only when **both** of the following are true:

1. The caller passed `skip_signature_check = 0`, **and**
2. The product's patch data does not delegate signature validation to the product's install script. Certain products utilize custom validation logic within their install scripts instead of the standard engine check. For these products, the engine-level steps below are bypassed; however, installer validation is still verified as part of the internal install process.

This delegation is controlled by the `skip_check_signature` field in the product's install metadata inside the OPSWAT patch data (e.g., patch.dat): it is not exposed through any API output, and no caller action is required.

When both conditions hold, the SDK performs these steps in order:

### [Step 1: Confirm signing information exists in the patch data](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#step-1-confirm-signing-information-exists-in-the-patch-data)

The SDK confirms it holds expected signing information for the product (vendor certificate chains and/or signer public keys, delivered with the patch data). If no signing information is available for the product, the call fails with `WA_VMOD_ERROR_CANNOT_VERIFY -1043`.

### [Step 2: Confirm the installer is signed](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#step-2-confirm-the-installer-is-signed)

The SDK checks the file's signing status using the platform's native code-signing verification: **Authenticode** on Windows, **macOS code signing** on macOS. An unsigned installer fails with `WAAPI_ERROR_INVALID_SIGNATURE -47` ("Unsigned installers.").
On Windows, both embedded (Authenticode) and catalog signatures are recognized.

### [Step 3: Validate the signature and match the expected vendor](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#step-3-validate-the-signature-and-match-the-expected-vendor)

The SDK validates that the signature is cryptographically valid and trusted, and that the signer matches the vendor expected for that product. If this fails, the call returns `WAAPI_ERROR_INVALID_SIGNATURE -47` ("File does not come from expected vendor or has been tampered").

- **Windows:** the embedded Authenticode signature is validated by the operating system, the certificate chain must be trusted, and the file must not have been modified since signing. The signer is then matched against the expected vendor in this order (any successful match passes):

  1. **Certificate chain**: subject and issuer of every certificate in the file's chain must equal one of the expected chains in the patch data (chain length included).
  2. **Thumbprint**: the end certificate's subject/issuer must match, and the SHA-1 thumbprint of the intermediate (level-1) certificate must equal the expected thumbprint.
  3. **Public key**: the signer certificate's public key bytes must equal one of the expected public keys.
- **macOS:** the code signature is validated across all architectures of the binary, and the signer's public key is compared against the expected public keys in the patch data.

**Online certificate revocation status is not checked on either platform.**

The signature verification is deliberately configured without revocation checking on both Windows and macOS. As a result, a signature made with a previously revoked certificate can still validate as long as the certificate chain is otherwise trusted and the file has not been modified since signing. This keeps verification deterministic on offline endpoints.

If any step fails, the installer is **never executed,** and the error above is returned to the caller.

### [Error reference](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#error-reference)

| Error | Condition |
| --- | --- |
| `WAAPI_ERROR_INVALID_INPUT_ARGS -20` | `skip_signature_check` is present but is not `0` or `1`, or its value could not be read. |
| `WA_VMOD_ERROR_CANNOT_VERIFY -1043` | The check is enabled but the patch data holds no signing information (public keys / certificate chains) for the product, so verification is impossible. |
| `WAAPI_ERROR_INVALID_SIGNATURE -47` | The installer is unsigned, its signature does not validate, or the signer does not match the expected vendor ("File does not come from expected vendor or has been tampered"). |

## [Verifying installer integrity when the signature check is skipped](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#verifying-installer-integrity-when-the-signature-check-is-skipped)

Independently of `skip_signature_check`, `InstallFromFiles` accepts an optional `expected_installer_sha256` input. When provided, the SDK computes the SHA-256 hash of the installer file and fails the call if it does not match the expected value, this check runs **regardless** of the `skip_signature_check` value and before any installation step.

**Recommendation**

If you keep the default `skip_signature_check = 1` (or install a product for which no signing data exists), pass `expected_installer_sha256` to ensure the file you downloaded is the exact file that gets executed.

## [**Products with rolling download URLs and newly released versions**](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#products-with-rolling-download-urls-and-newly-released-versions)

Some products publish a fixed download URL that always serves the latest installer (for example, Google Chrome's enterprise installer link). A new vendor release can therefore reach your endpoints before the OPSWAT patch data reflects the new version. In this situation the verification mechanisms behave differently:

- **Signature verification is version-independent.** With `skip_signature_check = 0`, the SDK validates the signer's identity and the file's integrity, not the file's version. A newer genuine installer signed by the expected vendor still passes verification. For rolling-URL products that have signing information in the patch data, this is the verification to rely on.
- **A checksum recorded for an earlier release will no longer match.** Passing an outdated `expected_installer_sha256` fails the call with `WAAPI_ERROR_HASH_MISMATCH -48`. This is the intended fail-closed behavior: compute or record the hash from the exact file you downloaded (for example, the SHA-256 returned by `GetLatestInstaller`), not from a previously cached release.
- **A product without signing information cannot use the signature check.** `skip_signature_check = 0` fails the call with `WA_VMOD_ERROR_CANNOT_VERIFY -1043` and there is no checksum fallback. To verify such a product, hash the downloaded file yourself and pass the value via `expected_installer_sha256`.

## [**Frequently asked questions**](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#frequently-asked-questions)

### [**Why is** `skip_signature_check` **not enabled by default?**](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#why-is-skip_signature_check-not-enabled-by-default)

The default is set to `1` to ensure compatibility with supported products that distribute unsigned installers or archive packages. Enabling verification by default would block these legitimate installations. You should manually enable the check (`0`) only when your specific integration requires the SDK to strictly enforce installer authenticity.

### [**Does skip_signature_check = 0 guarantee a revocation check?**](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#does-skip_signature_check--0-guarantee-a-revocation-check)

No, on neither Windows nor macOS. Revocation status is deliberately not queried (see the warning in [Step 3](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#step-3-validate-the-signature-and-match-the-expected-vendor)).

### [**Does InstallFromFiles check the installer against a checksum in the OPSWAT patch data?**](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#does-installfromfiles-check-the-installer-against-a-checksum-in-the-opswat-patch-data)

No. The only checksum check `InstallFromFiles` performs is the optional caller-provided `expected_installer_sha256` input. See [Verifying installer integrity when the signature check is skipped](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#verifying-installer-integrity-when-the-signature-check-is-skipped).

### [**Can an installation run with no verification at all?**](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#can-an-installation-run-with-no-verification-at-all)

Yes. With the default `skip_signature_check = 1` and no `expected_installer_sha256`, the SDK executes the installer without verifying its integrity or authenticity. See the recommendation in [Verifying installer integrity when the signature check is skipped](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#verifying-installer-integrity-when-the-signature-check-is-skipped).

### [**Why did the SDK not perform the engine-level check even though I passed** `0`**?**](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#why-did-the-sdk-not-perform-the-engine-level-check-even-though-i-passed-0)

For a small set of products, the patch data delegates installer validation to the product's install script; the engine-level steps are intentionally skipped for those products. The installer is still validated as part of the install flow, and the call's inputs, outputs, and error behavior are unchanged. See the note in [What the SDK verifies when skip_signature_check = 0](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#what-the-sdk-verifies-when-skip_signature_check--0).

There is currently no API output that identifies these products in advance. If you need to confirm which path was taken for a specific installation (for example, during a support investigation), enable SDK debug logging (see [Configuring Debug Logging](/docs/mdsdk/knowledge-base/configuring-debug-logging)) for the call and provide the v4debug log files to OPSWAT support: the log records whether the engine performed the signature verification itself.

### [**Does this apply to Linux?**](/docs/mdsdk/knowledge-base/skip-signature-check-in-installfromfiles-method#does-this-apply-to-linux)

No. On Linux, installer authenticity is governed by the platform package manager (e.g. APT repository GPG signing); the Authenticode-style engine verification described here applies to Windows and macOS.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

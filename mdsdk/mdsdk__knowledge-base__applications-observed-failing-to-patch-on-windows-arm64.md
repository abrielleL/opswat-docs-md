<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/applications-observed-failing-to-patch-on-windows-arm64 -->

# Applications Observed Failing to Patch on Windows ARM64

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Windows on ARM64 runs most x64 and x86 applications through emulation, so OESIS no longer blocks a patch only because its installer was built for a different OS architecture. `InstallFromFiles` runs the installer that `GetLatestInstaller` returns and leaves the architecture decision to the vendor's installer.

A small number of vendor installers refuse to install, or do not complete, on Windows ARM64. This article lists the applications where OPSWAT has observed this, explains what `InstallFromFiles` returns when it happens, and how to handle these products in your integration.

## How InstallFromFiles handles OS architecture

Earlier SDK builds checked the endpoint's OS architecture against an internal list before running some installers. For those patches, `InstallFromFiles` returned `WA_VMOD_ERROR_OS_ARCHITECTURE_NOT_SUPPORTED` (`-1046`) without running the installer, even though `GetLatestInstaller` had returned that same installer. An integration that called both methods on the same endpoint could therefore download a patch that `InstallFromFiles` then refused.

With the updated Windows engine, this SDK-side check is removed:

- `GetLatestInstaller` is unchanged and returns the installer that matches the product installed on the endpoint.
- `InstallFromFiles` runs that installer, whatever the endpoint's OS architecture.
- If the vendor installer does not support the architecture, the installer itself fails, and the SDK returns the vendor installer's own error so you can see why it failed.

Because the vendor installer makes the decision, a product starts patching successfully on ARM64 as soon as its vendor adds support, with no SDK or data change needed.

Engine update required

This behavior requires the updated Windows engine. Until you deploy it, `InstallFromFiles` continues to return `-1046` for the affected installers. Check the release notes for the engine version that includes this change.

## Applications with observed patching failures on ARM64

In OPSWAT testing on Windows 11 ARM64, OESIS observed the vendor installers for the following applications failing to install the product. Patching these products on ARM64 endpoints may fail in the same way. Results can differ with other installer versions or device configurations, so treat this list as a heads-up rather than a confirmed limitation.

| Product | Signature ID | Observed behavior on Windows 11 ARM64 |
| --- | --- | --- |
| FortiClient | 602 | MSI installer fails with exit code `1603` |
| Omnissa Horizon Client | 3124 | EXE installer fails with `0x80070643` |
| Cisco Secure Client | 3615 | MSI installer fails with exit code `1603` |
| pgAdmin 4 v7 (all users) | 3823 | Installer finishes, but `pgAdmin4.exe` is missing afterward |
| Sophos Connect | 3938 | MSI installer fails with exit code `1603` |
| Sage 50 Accounts (x64) | 3943 | EXE installer fails with exit code `1603` |
| Ivanti Application Control Agent | 4128 | MSI installer fails with exit code `1603` |
| TortoiseGit (x86) | 4129 | MSI installer fails with exit code `1603` |
| Ivanti Environment Manager Agent | 4130 | MSI installer fails with exit code `1603` |

This list reflects current testing and will be updated as vendors change their installers or new limitations are found. Applications not listed here, including x64 and x86 builds that previously returned `-1046` on ARM64, are expected to install through emulation.

## What InstallFromFiles returns when a patch fails

When the SDK runs an installer that does not support the endpoint's architecture, one of two outcomes is possible:

| Outcome | What happens | Result |
| --- | --- | --- |
| The vendor installer rejects the install | The installer exits with its own error, for example MSI `1603` | `InstallFromFiles` returns `WA_VMOD_ERROR_INSTALLATION_FAILED` (`-1034`) together with the vendor installer's error |
| The vendor installer does not exit | The install command keeps running until the default install timeout of 30 minutes | `InstallFromFiles` returns `WAAPI_ERROR_THREAD_TIMEOUT` (`-49`) |

In OPSWAT testing, the installers listed above failed with an error rather than hanging, but a timeout remains possible for any installer that does not handle an unsupported architecture cleanly.

## Recommendations for your integration

- On Windows ARM64 endpoints, match detected products against the signature IDs in the table above.
- For listed products on ARM64 endpoints, check whether the vendor offers a native ARM64 build and deploy that instead. If OESIS supports the ARM64 build, it is detected and patched under its own signature.
- Treat `-1034` with a vendor error such as `1603` on a listed signature as a likely vendor limitation rather than an SDK failure, and avoid retrying the same patch on every scan.
- If you want to avoid a failed install attempt, skip automatic patching for the listed signatures on ARM64 endpoints and report them for manual remediation.
- If an application that is not listed fails on ARM64 with a vendor error, or reaches the 30-minute timeout, open a support case with the signature ID, the SDK version, and the `InstallFromFiles` output.

## Related articles

- [Why OESIS Detects a Product but Only Patches Some of Its Variants](https://www.opswat.com/docs/mdsdk/knowledge-base/why-oesis-detects-a-product-but-only-patches-some-of-variants)
- [Mapping Architecture Values Between Compliance Output and Patching Metadata](https://www.opswat.com/docs/mdsdk/knowledge-base/mapping-values-between-GetVersion-and-patching-metadata)
- [Why can’t some supported products listed be patched automatically?](https://www.opswat.com/docs/mdsdk/knowledge-base/why-cant-some-supported-products-listed-be-patched-automatically)

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

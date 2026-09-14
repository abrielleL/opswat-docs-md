<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/mapping-values-between-GetVersion-and-patching-metadata -->

# Mapping Architecture Values Between Compliance Output and Patching Metadata

This article applies to MetaDefender Endpoint Security SDK releases deployed on Windows, Linux, MacOS.

## [Overview](/docs/mdsdk/knowledge-base/mapping-values-between-GetVersion-and-patching-metadata#overview)

This article explains how to map the `architecture.name` value returned from the SDK’s GetVersion to the `arch` field in `patch_associations.json` and the `architecture` field in the `download_links` array of `patch_aggregation.json`. This mapping ensures that patch selection and download processes work correctly across different platforms and architectures.

## [Table mapping](/docs/mdsdk/knowledge-base/mapping-values-between-GetVersion-and-patching-metadata#table-mapping)

| `architecture.name` **from GetVersion** **output** | `arch` **from** `patch_associations.json` | `download_links[].architecture` **from** `patch_aggregation.json` |
| --- | --- | --- |
| `aarch64` | `arm64` | `arm64` |
| `arm64` | `arm64` | `arm64` |
| `arm` | `arm`(*) | `arm`(*) |
| `Intel Itanium` | `Intel Itanium`(*) | `Intel Itanium`(*) |
| `i386` | `32-bit` | `32-bit` |
| `i386:x86-64` | `i386:x86-64`(*) | `i386:x86-64`(*) |
| `n/a` | Cannot map | Cannot map |
| `N/A` | Cannot map | Cannot map |
| `x32` | `32-bit` | `32-bit` |
| `x64` | `64-bit` | `64-bit` |
| `x86` | `32-bit` | `32-bit` |
| `x86_64` | `64-bit` or `x86_64` | `64-bit` |

(*) This value is not present in the current JSON file as there are no supported products for patching at this time. However, this field may be populated in future releases when additional products become available for patching support.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

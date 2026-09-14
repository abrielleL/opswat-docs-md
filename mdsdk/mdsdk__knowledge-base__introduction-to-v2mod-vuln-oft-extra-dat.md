<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/introduction-to-v2mod-vuln-oft-extra-dat -->

# Introduction to v2mod-vuln-oft-extra.dat

`v2mod-vuln-oft-extra.dat` is an optional companion file that restores additional data, such as CPE, to the lightweight `v2mod-vuln-oft.dat` database.

To use it, place the extra file in the same directory as the base file.

The engine will automatically detect and load the supplemental data during the offline database consumption process without requiring any code changes.

## [Problem](/docs/mdsdk/knowledge-base/introduction-to-v2mod-vuln-oft-extra-dat#problem)

Some customers rely on the smaller `v2mod-vuln-oft.dat` but still require additional details like CPE. Their only option today is to switch back to the full `v2mod.dat`, which reintroduces a heavy database, higher resource usage, and longer load times.

There is a need to provide additional information for `v2mod-vuln-oft.dat` users without losing the size and performance benefits of the shortened database.

## [What is this new file?](/docs/mdsdk/knowledge-base/introduction-to-v2mod-vuln-oft-extra-dat#what-is-this-new-file)

`v2mod-vuln-oft-extra.dat` is a supplemental database file that contains additional data, such as CPE, for the same CVEs that exist in `v2mod-vuln-oft.dat`.

The base file remains unchanged and continues to provide a compact offline CVE/CVSS dataset. The extra file only adds data; it never changes or removes anything in the base file.

## [How to use v2mod-vuln-oft-extra.dat](/docs/mdsdk/knowledge-base/introduction-to-v2mod-vuln-oft-extra-dat#how-to-use-v2mod-vuln-oft-extradat)

1. **Download the file.** Obtain `v2mod-vuln-oft-extra.dat` from the same source where you download your offline database packages, in the exact same directory as `v2mod-vuln-oft.dat`.
2. **Place the file.** Put `v2mod-vuln-oft-extra.dat` in the exact same directory as `v2mod-vuln-oft.dat` — the directory your integration already uses for offline databases.
3. **Verify the load.** After running `ConsumeOfflineVmodDatabase` (method ID `50520`), check the `loaded_files` array in the response to confirm both file paths and timestamps appear.
4. **Fallback behavior.** If the extra file is missing, the engine proceeds with the base file alone, no error occurs, and only CPE enrichment is absent.

## [Frequently asked questions](/docs/mdsdk/knowledge-base/introduction-to-v2mod-vuln-oft-extra-dat#frequently-asked-questions)

**Do I need to change my integration to use v2mod-vuln-oft-extra.dat?**

- No code changes are required if you already use `ConsumeOfflineVmodDatabase` (method ID `50520`) and `GetProductVulnerability` (method ID `50505`). Simply place the extra file alongside the base file. The new engine detects and uses it automatically.

**What happens if the extra file is missing or not recognized?**

- The system loads and serves data from `v2mod-vuln-oft.dat` as usual. There is no failure—only CPE enrichment is absent.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

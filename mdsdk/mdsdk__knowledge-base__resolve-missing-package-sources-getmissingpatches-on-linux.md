<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/resolve-missing-package-sources-getmissingpatches-on-linux -->

# Resolving Missing Package Source and Metadata Errors Returned by GetMissingPatches on Linux

This feature is currently in beta. Expect potential changes or improvements in future versions.

## [**Problem**](/docs/mdsdk/knowledge-base/resolve-missing-package-sources-getmissingpatches-on-linux#problem)

On Linux-based distributions, especially Ubuntu, the `GetMissingPatches` method may return `WAAPI_ERROR_MISSING_PACKAGE_RESOURCES` or `WAAPI_ERROR_MISSING_PACKAGE_INFORMATION`. This error prevents the retrieval of missing patch information during the method's invocation.

This issue is caused by **missing or corrupted package sources**. In certain cases, it occurs due to the initial machine setup lacking any configured sources, which leads to the error described above.

## [**Solution**](/docs/mdsdk/knowledge-base/resolve-missing-package-sources-getmissingpatches-on-linux#solution)

### [**Option 1:** Using `fetch_update_repository` flag](/docs/mdsdk/knowledge-base/resolve-missing-package-sources-getmissingpatches-on-linux#option-1-using--fetch_update_repository-flag)

Check Your Version

This input flag is only available starting with **SDK Engine version 4.3.3731.0 on Linux**. Please ensure you have upgraded to this version or later.

The optional input flag `fetch_update_repository` has been introduced in `GetMissingPatches` method to update the machine’s source package before retrieving the missing patches information.

- **Field Name**: `input.fetch_update_repository`
- **Field Type:** `boolean`
- **Description:** Instructs the SDK to update the repository before retrieving missing packages.
- **Behavior:**

  - If `fetch_update_repository` is provided and set to **true**, the SDK will attempt to update the package repository.
  - If `fetch_update_repository` is **omitted** or the value is **false**, the SDK will skip the repository update.

Warning

When using this parameter, ensure the process is running with `sudo` privileges and has an active internet connection. Otherwise, the operation may fail.

#### [**Usage Example**](/docs/mdsdk/knowledge-base/resolve-missing-package-sources-getmissingpatches-on-linux#usage-example)

WITHOUT updating source packageWITH source package update (required sudo permission)Copy{
"input": {
"method": 1013,
"signature": 200041
}
}{
"input": {
"method": 1013,
"signature": 200041,
"fetch_update_repository": true
}
}
### [**Option 2:** Manually update the source package](/docs/mdsdk/knowledge-base/resolve-missing-package-sources-getmissingpatches-on-linux#option-2-manually-update-the-source-package)

On Ubuntu, run the below command with `sudo` privileges to update the package sources. Then, re-invoke the `GetMissingPatches` method to retrieve the missing patch data.

Ubuntu TerminalCopysudo apt updateSupport

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

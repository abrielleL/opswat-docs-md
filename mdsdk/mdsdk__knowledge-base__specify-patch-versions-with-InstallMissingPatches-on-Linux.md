<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/specify-patch-versions-with-InstallMissingPatches-on-Linux -->

# How do I install specific patch versions with InstallMissingPatches on Linux?

This feature is currently in beta. Expect potential changes or improvements in future versions.

## [Problem](/docs/mdsdk/knowledge-base/specify-patch-versions-with-InstallMissingPatches-on-Linux#problem)

When a patch is released **between the calls to** `GetMissingPatches` **and** `InstallMissingPatches`, the SDK will install the **latest available version** of that patch — not necessarily the version the user originally expected.

This behavior may not align with some enterprise or compliance use cases, where customers require control over **which exact patch version** gets installed.

While most Linux package managers support installing **specific versions** of packages, this functionality was previously unavailable in the SDK. Currently, we support installing specific versions only for APT; support for other package managers such as DNF, YUM, and Zypper is planned and in the development queue.

## [Enhancement](/docs/mdsdk/knowledge-base/specify-patch-versions-with-InstallMissingPatches-on-Linux#enhancement)

To allow the installation of a specific patch version, a new optional input flag has been introduced in InstallMissingPatches method as follows:

- **Field Name:** `input.patches.version`
- **Field Type:** `string`
- **Purpose:** Allows specifying the exact version of a patch to install.
- **Behavior:**

  - If the `version` field is **provided**, the specified version will be installed (if available).
  - If the `version` field is **omitted**, the **latest available version** will be installed by default.

Note

The value of `version` must match a version string from the GetMissingPatches output or the `apt-cache madison <package>` output.

## [Usage](/docs/mdsdk/knowledge-base/specify-patch-versions-with-InstallMissingPatches-on-Linux#usage)

### [Install a Specific Patch Version](/docs/mdsdk/knowledge-base/specify-patch-versions-with-InstallMissingPatches-on-Linux#install-a-specific-patch-version)

JsonCopy{
"input": {
"method": 1014,
"signature": 200041,
"patches": [
{
"product": "wget",
"title": "wget",
"version": "1.21.2-2ubuntu1.1"
}
]
}
}
### [Install the Latest Patch Version (Default)](/docs/mdsdk/knowledge-base/specify-patch-versions-with-InstallMissingPatches-on-Linux#install-the-latest-patch-version-default)

JsonCopy{
"input": {
"method": 1014,
"signature": 200041,
"patches": [
{
"product": "wget",
"title": "wget"
}
]
}
}
### [Required Fields](/docs/mdsdk/knowledge-base/specify-patch-versions-with-InstallMissingPatches-on-Linux#required-fields)

- `product`: The name of the patchable product.
- `title`: The display name of the patch.
- `version`: *(Optional)* The exact version to install. If not provided, latest is used.

These values can be retrieved from the response of a GetMissingPatches method invocation.

## [How to Find Available Versions](/docs/mdsdk/knowledge-base/specify-patch-versions-with-InstallMissingPatches-on-Linux#how-to-find-available-versions)

You can use the following command to list available versions for a given package:

JsonCopyapt-cache madison <package_name>

Example (xxd package):

JsonCopyapt-cache madison xxd

This command shows all available versions for the specified package in a table format.

## [Updating the APT Repository](/docs/mdsdk/knowledge-base/specify-patch-versions-with-InstallMissingPatches-on-Linux#updating-the-apt-repository)

Before attempting to install a specific patch version, it is recommended to **fetch the latest repository index** by running the `sudo apt update` with a `priviledged` user, especially if the system has not run an update recently.

## [Installation Result States](/docs/mdsdk/knowledge-base/specify-patch-versions-with-InstallMissingPatches-on-Linux#installation-result-states)

During the installation process, the following result states may be returned for each patch:

| State | Description |
| --- | --- |
| `installed` | The specified version was successfully installed. Shown in `result.patches.version`. |
| `not_found` | The specified version does not exist in the package source. |
| `download_failed` | Download of the package failed (e.g., HTTP 404 or 503 error). |
| `cache_failed` | Package installation from cache failed (only applicable when `install_from_cache` is enabled). |
| `install_failed` | A general installation error occurred (e.g., corrupt package or install failure). |

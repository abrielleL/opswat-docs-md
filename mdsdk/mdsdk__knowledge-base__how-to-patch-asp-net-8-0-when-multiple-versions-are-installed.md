<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-to-patch-asp-net-8-0-when-multiple-versions-are-installed -->

# How to patch ASP.NET 8.0 using SDK when multiple versions are installed on a Windows machine?

This article is applied to MetaDefender Endpoint Security SDK releases on **Windows** with [**ASP.NET**](http://asp.net/) **8**.

## [**Problem**](/docs/mdsdk/knowledge-base/how-to-patch-asp-net-8-0-when-multiple-versions-are-installed#problem)

If multiple instances of ASP.NET 8.0 are installed on a Windows machine, OPSWAT SDK will always detect the instance with the highest version. This article will show you a workaround using Windows Update Agent - WUA (Signature: 1103) to apply Microsoft security updates for older instances.

For example, this machine has both ASP.NET **8.0.15** and **8.0.17** x64 installed, but SDK will only returns version 8.0.17.

## [**Using WUA to patch ASP.NET 8**](/docs/mdsdk/knowledge-base/how-to-patch-asp-net-8-0-when-multiple-versions-are-installed#using-wua-to-patch-aspnet-8)

Disclaimer

System patching workflow can only update the instance to the version that corresponds to the Microsoft security updates, which **may not always be the latest version**.

#### [**Workflow**](/docs/mdsdk/knowledge-base/how-to-patch-asp-net-8-0-when-multiple-versions-are-installed#workflow)

The suggested implementation is:

- Repeatedly run `GetLatestInstaller` and `InstallFromFiles` for the Windows Update Agent.
- Continue until the SDK returns the error code `WA_VMOD_ERROR_OUT_OF_RANGE`. This error code means there are no missing patches and the system is fully up-to-date.
- Once you receive the error code `WA_VMOD_ERROR_OUT_OF_RANGE`, the patching process is complete and no further updates are needed.

---

## [**Example**](/docs/mdsdk/knowledge-base/how-to-patch-asp-net-8-0-when-multiple-versions-are-installed#example)

Suppose your machine has the following installed:

- .NET SDK 8.0.115 x64 (Included runtimes: .NET Runtime 8.0.15, ASP.NET Core Runtime 8.0.15, .NET Desktop Runtime 8.0.15)
- ASP.NET core 8.0.16 x64

To ensure all versions are patched, follow this looped workflow using the SDK with Windows Update Agent (WUA, signature: 1103) by repeatedly invoking `GetLatestInstaller` and `InstallFromFiles`:

#### [Loop 1](/docs/mdsdk/knowledge-base/how-to-patch-asp-net-8-0-when-multiple-versions-are-installed#loop-1)

GetLatestInstallerInstallFromFilesCopyjson_in: {"method":50300,"token":"","signature":1103,"path":"","download":0}
json_out = {
"result" : {
"type_id" : 2,
"vendor" : "Microsoft",
"index" : 1,
"language" : "",
"patch_id" : 0,
"release_date" : "06/03/2025",
"release_note" : "",
"title" : "2025-06 .NET 8.0.17 Security Update for x64 Server (KB5061935)",
"analog_id" : "e53949e4-6291-46b0-8e44-833627df1f97",
"os_id" : 80,
"category" : "security_update",
"security_update_id" : "5061935",
"severity" : "important",
"product_name" : ".NET Framework",
"signature" : 1103,
"eula" : "",
"architecture" : "x64",
"url" : "http://download.windowsupdate.com/c/msdownload/update/software/secu/2025/06/aspnetcore-runtime-8.0.17-win-x64_71bce543f834826d414598a64cec5cabb3570929.exe",
"minimum_version" : "10.0.20348",
"optional" : false,
"expected_sha1" : [
"71BCE543F834826D414598A64CEC5CABB3570929"
],
"description" : "2025-06 .NET 8.0.17 Security Update for x64 Server (KB5061935)",
"timing" : 0,
"reboot_required" : 2,
"file_type" : "exe",
"timestamp" : "1755664656",
"code" : 0,
"method" : 50300
}
}json_in = {
"input": {
"method": 50301,
"signature": 1103,
"path": "aspnetcore-runtime-8.0.17-win-x64_71bce543f834826d414598a64cec5cabb3570929.exe",
"token": ""
}
}
json_out = {
"result" : {
"signature" : 1103,
"version" : "10.0.20348",
"language" : "",
"architecture" : "64-bit",
"require_restart" : 0,
"require_uninstall_first" : 0,
"require_close_first" : 0,
"log_paths" : [
"C:\\Windows\\Temp\\CBS_1755665000.log",
"C:\\Windows\\Temp\\dism_1755665000.log"
],
"blocking_processes" : [
],
"timestamp" : "1755664995",
"code" : 0,
"method" : 50301,
"timing" : 5031
}
}
#### [Loop 2](/docs/mdsdk/knowledge-base/how-to-patch-asp-net-8-0-when-multiple-versions-are-installed#loop-2)

GetLatestInstallerInstallFromFilesCopyjson_in: {"method":50300,"token":"","index":2,"signature":1103,"path":"","download":0}
json_out = {
"result" : {
"type_id" : 2,
"vendor" : "Microsoft",
"index" : 2,
"language" : "",
"patch_id" : 0,
"release_date" : "06/03/2025",
"release_note" : "",
"title" : "2025-06 .NET 8.0.17 Security Update for x64 Server (KB5061935)",
"analog_id" : "cd91f1df-a720-4309-8977-c20b76543032",
"os_id" : 80,
"category" : "security_update",
"security_update_id" : "5061935",
"severity" : "important",
"product_name" : ".NET Framework",
"signature" : 1103,
"eula" : "",
"architecture" : "x64",
"url" : "http://download.windowsupdate.com/c/msdownload/update/software/secu/2025/06/dotnet-sdk-8.0.117-win-x64_8010e93d09865912d7bca80da478a7643b705735.exe",
"minimum_version" : "10.0.20348",
"optional" : false,
"expected_sha1" : [
"8010E93D09865912D7BCA80DA478A7643B705735"
],
"description" : "2025-06 .NET 8.0.17 Security Update for x64 Server (KB5061935)",
"timing" : 0,
"reboot_required" : 2,
"file_type" : "exe",
"timestamp" : "1755664656",
"code" : 0,
"method" : 50300
}
}json_in = {
"input": {
"method": 50301,
"signature": 1103,
"path": "dotnet-sdk-8.0.117-win-x64_8010e93d09865912d7bca80da478a7643b705735.exe",
"token": ""
}
}
json_out = {
"result" : {
"signature" : 1103,
"version" : "10.0.20348",
"language" : "",
"architecture" : "64-bit",
"require_restart" : 0,
"require_uninstall_first" : 0,
"require_close_first" : 0,
"log_paths" : [
"C:\\Windows\\Temp\\CBS_1755665128.log",
"C:\\Windows\\Temp\\dism_1755665128.log"
],
"blocking_processes" : [
],
"timestamp" : "1755665030",
"code" : 0,
"method" : 50301,
"timing" : 97938
}
}

Patches were downloaded and installed of ASP.NET 8.0:

- aspnetcore-runtime-8.0.17-win-x64_71bce543f834826d414598a64cec5cabb3570929.exe
- dotnet-sdk-8.0.117-win-x64_8010e93d09865912d7bca80da478a7643b705735.exe

#### [Result](/docs/mdsdk/knowledge-base/how-to-patch-asp-net-8-0-when-multiple-versions-are-installed#result)

All installed ASP.NET 8.0 instances are now patched to the latest security update available via WUA.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/validation-endpoint/tool-check-the-prerequisites-of-the-mde-standalone-and-omva -->

# Tool check the prerequisites of the MetaDefender Endpoint Validation (MDE Validation) and OMVA

## 1. Introduce

Welcome to the MDE Prerequisites Inspector! This tool is designed to help verify whether your machine meets the minimum system requirements to run MetaDefender Endpoint (MDE) Validation or OPSWAT Media Validation Agent (OMVA) on Windows. It checks for features such as SHA-2 code signing support and specific Windows API availability.

## 2. Using the application

- The latest version of the MDE Prerequisites Inspector: [Download](https://installer-cdn.opswat.com/kiosk/MDE/MDEPrerequisitesInspector.exe)

### **2.1** **Launching the Application**

- Run the execute application with command line:

![](https://uploads.developerhub.io/prod/2x2P/w6i1eh3l56vy36mmwpsc3bmniuc4cs6m8veoo386sitor3ues3dn16z0fm9vkm9v.png)

- There are 2 options for “app” param, which are “standalone“ and “omva”
- “app” param is equal to “standalone” by default. This means that if the param is not present or param is not equal to “omva”, the application will check prerequisite of MDE standalone.

![Sample to check if machine can install MDE validation](https://uploads.developerhub.io/prod/2x2P/x4vib8h89s0s7vtp471u6ywzbb9nl36kggygrl3ic4bnsya406u193wo1zwof2gs.png)

![Sample to check if machine can install OMVA](https://uploads.developerhub.io/prod/2x2P/s6ao955p0me7gwqa10gkv3fqs5xjkorrrhw7udalg4mvw6xgvbtbguy9akts7ve1.png)

### **2.2 Main features**

The MDE Prerequisites Inspector offers the following checks:

1. **SHA-2 Code Signing Support:** This check verifies whether your system has SHA-2 support enabled, which is essential for secure software installations.
2. **Windows API Availability:** The tool checks for the following APIs:
   - `SetDefaultDllDirectories`
   - `AddDllDirectory`
   - `RemoveDllDirectory`

### **2.3** **Return codes and recommended KB**

| **Return Code in Decimal** | **Meaning** | **Recommend install KB** |
| ---- | ---- | ---- |
| 0 **MDE_OK** | Successful completion. |  |
| -1 **MDE_ERR_WINAPI_FUNCTION_NOT_EXIST** | Some WinAPIs is not exist in your machine | KB3063858 (Wins 7) |
| -2 **MDE_ERR_WINAPI_HANDLE_NOT_EXIST** | `Kernel32.dll` is missed from your machine | KB3063858 (Wins 7) |
| -19 **MDE_ERR_WINAPI_UNKNOWN** |  | KB3063858 (Wins 7) |
| -21 **MDE_ERR_DRIVER_ACTION_NOT_SIGNED** | The signature was not found or not recognized. | KB3033929 (Wins 7) |
| -22 **MDE_ERR_DRIVER_ACTION_VERIFY** | WinVeryTrust return TRUST_E_NOSIGNATURE  but not TRUST_E_SUBJECT_FORM_UNKNOWN TRUST_E_PROVIDER_UNKNOWN | KB3033929 (Wins 7) |
| -23 **MDE_ERR_DRIVER_ACTION_EXPLICIT_DISTRUST** | The certificate is explicitly distrusted by the system. | KB3033929 (Wins 7) |
| -24 **MDE_ERR_DRIVER_ACTION_SUBJECT_NOT_TRUSTED** | The subject of the signature is not trusted. | KB3033929 (Wins 7) |
| -25 **MDE_ERR_DRIVER_ACTION_UNTRUSTEDROOT** | The certificate chain leads to an untrusted root certificate authority. | KB3033929 (Wins 7) |
| -39 **MDE_ERR_DRIVER_ACTION_UNKNOWN** |  | KB3033929 (Wins 7) |
| -41 **MDE_ERR_RESOURCE_FIND** | Can not save resource (sample sys file use for verify signature) |  |
| -42 **MDE_ERR_RESOURCE_LOAD** | Can not load resource (sample sys file use for verify signature) |  |
| -43 **MDE_ERR_RESOURCE_GETSIZE** | Can not get size of resource (sample sys file use for verify signature) |  |
| -44 **MDE_ERR_RESOURCE_LOCK** | Can not lock resource to get data (sample sys file use for verify signature) |  |
| -45 **MDE_ERR_RESOURCE_UNKNOWN** |  |  |
| -61 **MDE_ERR_CLI_INVALID** | CLI catches invalid command |  |
| -1000 **MDE_ERR_UNKNOWN** | Unknown error |  |

## 3. System requirements

- Windows 7 and later

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)

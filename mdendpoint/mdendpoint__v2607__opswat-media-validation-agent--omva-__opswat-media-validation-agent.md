<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/opswat-media-validation-agent--omva-/opswat-media-validation-agent -->

# OPSWAT Media Validation Agent (OMVA)

The OPSWAT Media Validation Agent (OMVA) is a lightweight tool that is deployed on Windows endpoints ensuring that the contents of media can only be accessed if it has been processed & allowed by MetaDefender Kiosk.

With the [media manifest feature](https://www.opswat.com/docs/mdkiosk/operating/selecting-a-server-to-process-files#include-media-manifest-on-user-media)  enabled, after media is processed by MetaDefender Kiosk, it will contain a media manifest that is digitally signed and hashes of all the clean and approved files. When an endpoint has OMVA installed, any media that is inserted is first checked for a valid digital signature from the Kiosk and then a hash check is performed verifying that the contents of the media have not been altered.

> **Limitation**
>
> Encrypted devices supported by Kiosk are not supported by OPSWAT Media Validation Agent (OMVA)

---

## Supported Operating Systems

Two different flavors of OMVA are offered in My OPSWAT Portal for specific deployment platforms:

![](https://uploads.developerhub.io/prod/2x2P/y5qksk10ltplka6dwb7fiah8s0p7zezxoij3kepsxgyjh7c1nnu3re1bud119wvk.png)

### OMVA - Windows XP SP3, 7 and above

OMVA is supported on the following operating systems:

| OS version | 32-bit | 64-bit | Note |
| ---- | ---- | ---- | ---- |
| Windows XP SP3 | Yes | OS version is not available in 64-bit |  |
| Windows 7* | Yes | Yes |  |
| Windows 8 | Yes | Yes |  |
| Windows 8.1 | Yes | Yes |  |
| Windows 10 | Yes | Yes |  |
| Windows 11 | OS version is not available in 32-bit | Yes |  |
| Windows Server Small Business Server standard FE (version: 2011 Standard) | Yes | Yes | Requires KB2533623 installed ([http://go.microsoft.com/fwlink/p/?linkid=217865](http://go.microsoft.com/fwlink/p/?linkid=217865)) |
| Windows Server 2008 R2* | Yes | Yes | No support for Windows Server 2008 |
| Windows Server 2012* | OS version is not available in 32-bit | Yes |  |
| Windows Server 2012 R2* | OS version is not available in 32-bit | Yes |  |
| Windows Server 2016* | OS version is not available in 32-bit | Yes |  |
| Windows Server 2019* | OS version is not available in 32-bit | Yes |  |
| Windows Server 2022* | OS version is not available in 32-bit | Yes |  |

> ***NOTE**
>
> Windows 7 and Windows Server OS require KB4474419 installed ([https://support.microsoft.com/en-us/help/4474419/sha-2-code-signing-support-update](https://support.microsoft.com/en-us/help/4474419/sha-2-code-signing-support-update))

### OMVA - Windows 7 SP1 (without KBs)

OMVA is supported on the following operating system (32/64-bit):

- Windows 7 SP1

This build is specific for Windows 7 deployments that cannot install the required KB to enable SHA2 code signing support.

---

## Minimum System Requirements

- **Processor:** 2 Cores / 2 Logical Processors
- **Memory:** 2 GB RAM

---

## Installing the agent

The OMVA installer can be obtained from [My OPSWAT](https://my.opswat.com/)  under the MetaDefender Endpoint page. To do so, follow the steps below:

**Step 1:** Go to [My OPSWAT](https://my.opswat.com/portal/home) > *Product Downloads* > *MetaDefender Endpoint*

![](https://uploads.developerhub.io/prod/2x2P/4pp7jipp6z6z0nihgbme9x9g747i4277czbnw768ak76k5bxb12qv5z04mcb0xdn.png)

**Step 2:** Navigate to the OPSWAT Media Validation Agent tab, select the intended Platform and download the agent

![](https://uploads.developerhub.io/prod/2x2P/j2zfdwqpz8qtoad6jt8w3qas4dy4umgtiqbw6kdh573edungdbdhqib42c7as6tj.png)

Run the .msi obtained on the Windows endpoint.

![](https://uploads.developerhub.io/prod/2x2P/1s9dv8rd247cla69mr07pai4fjw4rsis84iux6ol97e8lpb2idi5jogplkvqs2xr.png)

The Agent must be provided with the certificates it should consider trusted. The Agent will look in `%ALLUSERSPROFILE%\OPSWAT\.ssh\` to locate all trusted certificates.

If the trusted certificate is not in the directory, the Agent can also verify certificate trust if the root Certificate Authority certificate is installed. OPSWAT recommends automating the deployment and installation of trusted certificates to the client using an AD Push or similar technique. A Certificate Authority certificate can also be installed for an individual end-point by copying the .crt file over, right clicking on it, and selecting `Install Certificate`.

![](https://uploads.developerhub.io/prod/2x2P/jivfqkpl00bwfzt5to01y3xzh1lzlwwchumhk4ok2yitmoqawms4v7k45rrbc114.png)

---

## User guide

### Media verification

Insert the media to the endpoint.

The OPSWAT Media Validation Agent will begin checking the media according to these steps:

1. Looks for an OPSWAT Media Manifest file on the media
2. Checks to make sure the Certificate that signed the media manifest is trusted
3. Checks each file on the removable media against the media manifest to make sure it has not been modified

![](https://uploads.developerhub.io/prod/2x2P/rgze81n4a8j4lxbyd643vsupjq0uz8szq7f1m1e9ypzwxsahbfieywc6zjdzv1ld.png)

### Results of verification

If the manifest is found to have all files on the media recorded and unmodified, the media will be allowed to be accessed on the endpoint:

![](https://uploads.developerhub.io/prod/2x2P/4rmigord07awxtv4i3fab0ez5a7ohkydsto8d3cjolzgw9grgiiel5dwlpfkg106.png)

If the manifest is found to be invalid or files on the media are found to be missing/modified from the manifest, the media will be blocked from being accessed on the endpoint:

![](https://uploads.developerhub.io/prod/2x2P/vjxi9wzi3py8w28q6t6p69mg4vqg2icsoqu8qljrtn3vc47zd8uaufoh1c57pfqq.png)

![](https://uploads.developerhub.io/prod/2x2P/49n2yvbmnbasx3eit0r8hpthopfdng684huncsv70u8wqfdqmb0c1ie9v6k0tp7h.png)

> **Info**
>
> The Validation Agent takes an "all-or-nothing" approach. Any invalid file or manifest will result in the entire media being blocked. There is no access to a subset of valid files.

---

## Logging

OMVA logs JSON formatted messages of its operation. This can be used to determine the validation ran on the system and identify any media that was blocked. Logging can be found in the OMVA install directory:

- Windows XP: %ALLUSERSPROFILE%\Application Data\OPSWAT\OPSWAT-OMVA
- Other Windows versions: %PROGRAMDATA%\OPSWAT\OPSWAT-OMVA

When extracting logs from the file, the JSON objects must be wrapped within square brackets "**[ ]"** to allow for proper parsing.

```json
{
    "date": utc formatted string
    "event_code": event code integer
    "level": log level string
    "message": message string
    "hostname": system hostname string
    "username": username of logged-in user string
}
```

| Event code | Description | Notes |
| ---- | ---- | ---- |
| 0 | Validation begin - USB inserted | contains additional `user_data` string field in the json message |
| 1 | File result error |  |
| 2 | Validation end - Media validation result |  |
| 3 | Signature Result |  |

```json
{
    "date": "2021-04-22T17:28:11Z",
    "event_code": 0,
    "level": "info",
    "message": "USB inserted - Volume{0f1895d7-d714-4030-9b2c-3aeacb631d1b}",
    "hostname": "Workstation3186",
    "username": "company/userA",
    "user_data": "[Kiosk] SessionID: 81E60795-67D8-4A34-8792-90D6E403D039 || User: abc || System: Kiosk1 || Device ID: SCSI\\DISK&VEN_MSFT&DISK\\2&1F4FFE&0&0001 || Start Time: 2021-07-08 16:10:01"
},
{
    "date": "2021-04-22T17:28:15Z",
    "event_code": 1,
    "level": "info",
    "message": "G:\\files\\spreadsheet.xlsx - File not found in Media Manifest",
    "hostname": "Workstation3186",
    "username": "company/userA"
},
{
    "date": "2021-04-22T17:28:20Z",
    "event_code": 2,
    "level": "info",
    "message": "Unable to mount drive, please rescan with MetaDefender Kiosk",
    "hostname": "Workstation3186",
    "username": "company/userA"
}
```

---

## Configuration

Registry configuration:

For Windows 32 bit: `HKLM\SOFTWARE\OPSWAT\OPSWAT-OMVA`

For Windows 64 bit: `HKLM\SOFTWARE\WOW6432Node\OPSWAT\OPSWAT-OMVA`

| Key | Type | Description |
| ---- | ---- | ---- |
| days_trusted | REG_SZ or REG_ DWORD | The maximum days to use a media manifest result If blank or omitted, the manifest is trusted forever |

---

## Uninstalling OMVA

Uninstalling the agent requires the password: `Opswat1234!` to successfully complete

---

## OMVA Tool

Run `OPSWAT-OMVA-Tool.exe` before installing OMVA on endpoints.

![](https://uploads.developerhub.io/prod/2x2P/jcie63sunh1hl9rtzjnrezw1iaxmejrw5vw4nf53lbbjzxcdgnc714ux8hxytn3s.png)

Enter in the new password to configure. Click `Generate` to create a new filename for the OMVA installer. Download the new OMVA installer from the Resources page. Copy the `New File Name` and rename the installer. Installing this renamed file on all endpoints will ensure the uninstall password adheres to what was configured in the tool.

When the ***"Enable boot protection*****"** option is checked, the OMVA application will block access to any external removable media drives that are connected before the system boots up.

To update existing installations, the previous OMVA must be uninstalled with the default password. Then install the newly renamed OMVA installer.

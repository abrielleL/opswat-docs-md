<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-can-i-update-to-the-lastest-domain-certificate- -->

# How can I update to the lastest domain certificate?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS and Linux systems.

> **Please note:**
>
> Since 23 March 2022, customers are no longer permitted to use the cross-domain API features on their devices if their domain certificates are out of date.
>
> In such cases, users may also be blocked from accessing certain private resources that are integrated with the cross-domain API feature.

## Which MetaDefender Endpoint versions include the latest domain certificate?

At the time of writing, OPSWAT updated and released the latest client on 20 September 2022, but the latest domain certificate was first included in the version released on 18 January 2022.

It follows that all OPSWAT persistent and on-demand MetaDefender Endpoint releases following the 18 January 2022 release have included or will include the latest domain certificate.

If your version succeeds the releases listed below, your domain certificate will be up to date.

|  | Windows | Mac | Linux |
| ---- | ---- | ---- | ---- |
| **Persistent** | 7.6.535.0 | 10.4.366.0 | deb: 15.4.63.0 rpm: 15.6.62.0 |
| On-demand | 7.3.665.0 | 10.5.297.0 | N/A |

## How do I update to the latest domain certificate?

### **On-Demand Client**

In order to update to the latest domain certificate and continue using the cross-domain API features, users must update their on-demand MetaDefender Endpoint to any version following **7.3.665.0** for Windows, or **10.5.297.0** for macOS.

### **Persistent Client**

In order to update to the latest domain certificate and continue using the cross-domain API features, persistent Client users have three possible options.

- One option is to enable **Automatic Updates** to the latest version.
- Another option is to configure **Custom Checks** so that the latest domain certificates will be downloaded as soon as they are released.
- The last option is to download the latest domain certificate and **Manually Update** it to their devices.

#### Option 1: enable Automatic Updates to the latest persistent Client version

1. As administrator, go to the **MetaDefender IT-OT Access Console**, then navigate to **Settings>Global>Device Agents** and enable the option to **Automatically update to a specific version**, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/zw6xcshzl19hnprenj1q6vq2ejhlxil958suj1xv2acoexvalu7uuqjz9w7uc5dh.png)

2. Once this setting is enabled, MetaDefender Endpoint will automatically upgrade to the latest available version, with no user action required.
3. If an endpoint user’s device has not received the latest upgrade, the user should contact their administrator to download and install the latest MetaDefender Endpoint to that device.

#### Option 2: use the Custom Check feature to automatically download the latest domain certificate to the endpoint user’s device

1. As administrator, use the relevant script below to enable automatic domain certificate checks and updates on your managed endpoints.

Windows:

```powershell
# Description:
#     Purpose: Update the jsonp_server.crt file for Windows persistent if it is not up-to-date
#
# Note:
#     Supports for the Powershell 2.0 on Windows 7
#     Support for Windows 32-bit and Windows 64-bit

$Url = "https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/jsonp_server.crt"
$DownloadPath = "C:\"
$FileName = "jsonp_server.crt"

$Is64BitOS = $False
if ((Get-WmiObject win32_operatingsystem | Select-Object osarchitecture).osarchitecture -like "64*")
{
    $Is64BitOS = $True
}

$OriginalCertificateFileHash = "AE-53-68-47-CD-24-39-6C-36-37-FB-0A-39-92-83-D3"

$StoredCertificateFile = "C:\Program Files (x86)\OPSWAT\GEARS Client\jsonp_server.crt"
if ($Is64BitOS -eq $False)
{
    $StoredCertificateFile = "C:\Program Files\OPSWAT\GEARS Client\jsonp_server.crt"
}

$HashAlgorithm = New-Object -TypeName System.Security.Cryptography.MD5CryptoServiceProvider

$StoredCertificateFileHash = [System.BitConverter]::ToString($HashAlgorithm.ComputeHash([System.IO.File]::ReadAllBytes($StoredCertificateFile)))

Write-Output "[output]"

if ($OriginalCertificateFileHash -ne $StoredCertificateFileHash)
{
	(New-Object Net.WebClient).DownloadFile($Url, "$DownloadPath\$FileName")

	$DownloadedFileExists = Test-Path $DownloadPath\$FileName

	if ($DownloadedFileExists -eq $True)
	{
        $Destination = "C:\Program Files (x86)\OPSWAT\GEARS Client"
        if ($Is64BitOS -eq $False)
        {
            $Destination = "C:\Program Files\OPSWAT\GEARS Client"
        }

        $JsonpServerFileExists = Test-Path $Destination\$FileName
        if ($JsonpServerFileExists -eq $True)
        {
            Copy-Item $DownloadPath\$FileName -Destination $Destination
        }

		Remove-Item $DownloadPath\$FileName

		Write-Output "result=1"
		Write-Output "msg=File $FileName was updated"

		Stop-Process -Name "owcjls" -Force
	}
	else
	{
		Write-Output "result=0"
		Write-Output "msg=File $FileName not found"
	}
}
else
{
	Write-Output "result=1"
	Write-Output "msg=File $FileName is up-to-date"
}
```

**MacOS:**

```powershell
#!/bin/sh -x

result=1
msg=""
url="https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/jsonp_server.crt"

path="/Applications/OPSWAT GEARS Client/OPSWAT GEARS.app/Contents/Resources/jsonp_server.crt"
file_name="jsonp_server.crt"

if [ -f "$path" ]
then
	crt_hash=$(md5 "$path")
	echo $crt_hash

	if [ ! "$crt_hash" = "MD5 ($path) = ae536847cd24396c3637fb0a399283d3" ]
	then
		msg="File $file_name was updated"
		echo $msg

		curl -o "$path" $url

		killall opswat-gears-od
	else
		msg="File $file_name is up-to-date"
		echo $msg
	fi
else
	msg="File $file_name not found"
	echo $msg
fi

echo [output]
echo result=$result
echo msg=$msg
```

**Linux:**

```powershell
#!/usr/bin/env bash

result=1
msg=""
url="https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/cross_domain_pkcs12.crt"
path="/usr/bin/opswatclient/lib"
file="/usr/bin/opswatclient/lib/cross_domain_pkcs12.crt"

if [ -f "$file" ]
then
	crt_hash=$(md5sum "$file" | awk '{ print $1 }')
	echo $crt_hash

	if [ ! "$crt_hash" = "9b4d50fe53e8ab670c7d6d9094047e96" ]
	then
		msg="File $file was updated"
		echo $msg

        rm $file

		wget $url -P "$path"

		systemctl restart opswatclient
	else
		msg="File $file is up-to-date"
		echo $msg
	fi
else
	msg="File $file not found, downloaded new certificate"

    wget $url -P "$path"

	systemctl restart opswatclient

	echo $msg
fi

echo [output]
echo result=$result
echo msg=$msg
```

2. Administrators can apply the Custom Check feature on individual policies via the MetaDefender IT-OT Access Console by navigating to Policy Management>Policies>Chosen Policy>Deep Compliance and enabling the Custom Check option, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/dlz1dp176vsdwx8jhgnzm9mr5zllobxcdo058xbjrg3ajvla06fuyaf5lpabfyju.png)

#### Option 3:

1. Download the latest domain certificate for your OS by clicking the relevant link below.

| Windows/MacOS | Linux |
| ---- | ---- |
| [https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/jsonp_server.crt](https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/jsonp_server.crt) | [https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/cross_domain_pkcs12.crt](https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/cross_domain_pkcs12.crt) |

2. Once downloaded, the user must replace their expired certificate by copying the new certificate file to the installation directory of the MetaDefender Endpoint. The installation directory locations for each OS are listed below.

| Windows | Mac | Linux |
| ---- | ---- | ---- |
| ***C:\Program Files (x86)\OPSWAT\GEARS Client*** | ***/Applications/OPSWAT GEARS Client/OPSWAT GEARS.app/Contents/Resources/*** | ***/usr/bin/opswatclient/lib/*** |

3. Finally, the user will need to either restart the MetaDefender Endpoint service or restart their device to apply their updated domain certificate.

> **Support:**
>
> If you have followed the instructions above but are **Still Unable To Use Cross-Domain API Features Or Access Assiated Private Resources**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)

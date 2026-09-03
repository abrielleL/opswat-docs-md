<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/account-policy -->

# Account Policy

| API version | 2.0 |
| --- | --- |
| Last Update | 6/15/2015 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use this API to retrieve default device policy

## [API URL](/docs/macloud-sdp/developer-guide/account-policy#api-url)

https://gears.opswat.com/o/api/v2/account/policy
## [Request Parameters](/docs/macloud-sdp/developer-guide/account-policy#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | Header | Yes | access token which archived from OAuth authentication step |  |

## [Response HTTP Code](/docs/macloud-sdp/developer-guide/account-policy#response-http-code)

See [APIs](/docs/macloud-sdp/developer-guide/apis)

## [Response Parameters](/docs/macloud-sdp/developer-guide/account-policy#response-parameters)

| Key | Datatype | Description |
| --- | --- | --- |
| policy | object | Policy configuration |
| policy.<category> | object | detailed configuration of a category |
| policy.<category>.<policy> | object | detailed policy in a category |
| policy.<category>.<policy>.desc | string | policy description |
| policy.<category>.<policy>.alert | int | Indicate if this policy is considered as an issue |
| policy.<category>.<policy>.critical | int | Indicates if this policy is considered as a critical issue |
| policy.<category>.<policy>.remediation | int | Indicates if a remediation option is turned on |
| policy.<category>.apply_to | object | Indicates if this option is applying to any device type |
| policy.<category>.apply_to.laptop | int | Indicates if this option is applying to laptop devices |
| policy.<category>.apply_to.desktop | int | Indicates if this option is applying to desktop devices |
| policy.<category>.apply_to.server | int | Indicates if this option is applying to server devices |
| policy.<category>.apply_to.vm | int | Indicates if this option is applying to virtual machine devices |

## [Example](/docs/macloud-sdp/developer-guide/account-policy#example)

**Request Example**

https://gears.opswat.com/o/api/v2/account/policy?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234

**Response Example**

{
"policy": {
"Cloud_Storage": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if Running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if Installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
},
"Developer_Tool": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if Running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if Installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
},
"Hard_Disk_Encryption": {
"EncryptionAlgorithm": {
"desc": "Consider unencrypted unless using: ",
"alert": 1
},
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"PartiallyEncrypt": {
"desc": "Consider volumes encrypted when product reports \"Partially encrypted\"",
"alert": 1
},
"Installed": {
"desc": "Report if no encryption application is installed",
"critical": 1,
"alert": 1
},
"AdditionalVolume": {
"desc": "Report if additional volumes are not encrypted by an approved application",
"critical": 1,
"alert": 1
},
"SystemVolume": {
"desc": "Report if system volume is not encrypted by an approved application",
"critical": 1,
"alert": 1
},
"SuspendedEncrypt": {
"desc": "Consider volumes encrypted when product reports \"Encryption protection suspended\"",
"alert": 1
}
},
"Uninstaller": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if Running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if Installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
},
"Antiphishing": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"BrowserProtection": {
"desc": "Require at least one antiphishing product to be enabled",
"critical": 1,
"alert": 1
}
},
"Media_Player": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if Running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if Installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
},
"Patch_Mangement_Agent": {
"Enabled": {
"desc": "Report if third party patch client is disabled",
"critical": 1,
"alert": 1
},
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Installed": {
"desc": "Report if no third party patch client is installed",
"critical": 1,
"alert": 1
}
},
"Toolbars": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if Running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if Installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
},
"SystemSecurity": {
"apply_to": {
"vm": 1,
"laptop": 0,
"desktop": 0,
"server": 0
},
"Passcode": {
"desc": "Report if passcode is disabled",
"critical": 0,
"alert": 1
},
"OutOfDate": {
"desc": "Report if system is not authentic",
"critical": 0,
"alert": 1
}
},
"PublicFileSharing": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if public file sharing is running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if public file sharing application is installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
},
"OSUpdate": {
"Enabled": {
"desc": "Report if automatic updating is disabled",
"critical": 1,
"alert": 1
},
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"OutOfDate": {
"desc": "Report if OS is not up-to date",
"critical": 1,
"alert": 1
}
},
"Recording_Web_Meeting": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if Running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if Installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
},
"Firewall": {
"Enabled": {
"desc": "Require at least one personal firewall to be enabled",
"critical": 1,
"alert": 1,
"remediation": 1
},
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
}
},
"Instant_Messegener": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if Running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if Installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
},
"Antivirus": {
"Enabled": {
"desc": "Require real time protection from at least one antivirus product",
"critical": 0,
"alert": 1,
"remediation": 0
},
"DefinitionTime": {
"desc": "Require at least one antivirus product to have definitions less than 3 days old",
"critical": 0,
"alert": 1,
"remediation": 0
},
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Installed": {
"desc": "Report if no antivirus application is installed",
"critical": 0,
"alert": 1
},
"ThreatsDetected": {
"desc": "Report if at least one antivirus has detected any threats in the last 7 days",
"critical": 0,
"alert": 1
},
"SystemScan": {
"desc": "Require full system scan from at least one antivirus in the last 7 days",
"critical": 0,
"alert": 1
}
},
"Cleaner_Optimizer": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if Running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if Installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
},
"VPN_Client": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if Running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if Installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
},
"Hard_Drive": {
"apply_to": {
"vm": 0,
"laptop": 0,
"desktop": 0,
"server": 0
},
"AvailableSpace": {
"desc": "Report if available hard drive space is less than 10%",
"critical": 1,
"alert": 1
}
},
"BackupClient": {
"Activity": {
"desc": "Report if no backup activity in the last 3 days",
"critical": 1,
"alert": 1
},
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 0,
"server": 1
},
"Installed": {
"desc": "Report if no backup application is installed",
"critical": 1,
"alert": 1
}
},
"Unclassified_PUA": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if Running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if Installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
},
"System": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Password": {
"desc": "Report if password protection is off",
"critical": 1,
"alert": 1
},
"LockScreen": {
"desc": "Report if lock screen timeout is over 10 minutes",
"critical": 1,
"alert": 1
}
},
"Remote_Control": {
"apply_to": {
"vm": 1,
"laptop": 1,
"desktop": 1,
"server": 1
},
"Running": {
"desc": "Report if Running",
"critical": 1,
"alert": 1,
"remediation": 1
},
"Installed": {
"desc": "Report if Installed",
"critical": 1,
"alert": 1,
"remediation": 1
}
}
}
}

<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/email-notifications -->

# Email Notifications

You can turn on email notifications on MetaDefender IT Access to receive notifications when certain events occur. The notifications can be sent in HTML or JSON format.

## [Turn on/Update email notifications](/docs/macloud-sdp/configuration---management/email-notifications#turn-onupdate-email-notifications)

1. Log into MetaDefender IT Access console
2. Navigate to **Settings > Notification Groups > Emails**
3. Input the emails you would like MetaDefender IT Access sends a notification to. Each email should be on it's own line.
4. Choose a notification format.
5. Select events that trigger an email notification.
6. Click **Save** and confirm your PIN to save changes.

Info

- More information may be added into the email content for both HTML and JSON.
- The content in HTML format is only the main content of notification. The full notification includes other static messages.
## [Admin logged on/off](/docs/macloud-sdp/configuration---management/email-notifications#admin-logged-onoff)

Subject: [MetaDefender IT Access] Admin logged on: First_Name ([email@yourdomain.com](https://onlinehelp.opswat.com/metaaccess/mailto:email@yourdomain.com))

| **Event:** | **Admin logged on** |
| --- | --- |
| Admin Name: | <admin name> |
| Admin Email: | [<](https://onlinehelp.opswat.com/metaaccess/mailto:vtran@opswat.com)email> |
| Details: | Admin logged on |
| Time: | <date and time> |

JsonCopy{
"event": "Admin logged on",
"first_name": "First Name",
"last_name": "Last Name",
"email": "email@yourdomain.com",
"details": "Admin logged on",
"time": "Oct 02, 2017 10:39 AM (UTC)",
}
## [Admin made configuration change](/docs/macloud-sdp/configuration---management/email-notifications#admin-made-configuration-change)

Subject: [MetaDefender IT Access] Admin made configuration change: First_Name ([email@yourdomain.com](https://onlinehelp.opswat.com/metaaccess/mailto:email@yourdomain.com))

| **Event:** | **Admin made configuration change** |
| --- | --- |
| Admin Name: | <Admin Name> |
| Admin Email: | [email@yourdomain.com](https://onlinehelp.opswat.com/metaaccess/mailto:email@yourdomain.com) |
| Details: | Global Settings (Privacy Setting local IP address is turned off) Global Settings (Privacy Setting MAC address is turned off) |
| Time: | Oct 12, 2017 10:22 AM (UTC) |

JsonCopy{
"event": "Admin made configuration change policy Default",
"first_name": "First Name",
"last_name": "Last Name",
"email": "email@yourdomain.com",
"details": ["Issue Settings (Encryption - Report if additional volumes are not encrypted by an approved application)"],
"time": "Oct 02, 2017 10:39 AM (UTC)"
}
## [Account has X% license(s) left](/docs/macloud-sdp/configuration---management/email-notifications#account-has-x-licenses-left)

Subject: [MetaDefender IT Access] Account is running out of licenses

| **Event:** | **Account is running out of licenses** |
| --- | --- |
| Account Name | OPSWAT IT |
| Account Email: | [it@opswat.com](https://onlinehelp.opswat.com/metaaccess/mailto:it@opswat.com) |
| Device Limit | 1000 |
| Device Monitored | 990 |
| Number of license left | 10 |
| Action Needed | Please contact [OPSWAT](https://www.opswat.com/contact) in order to upgrade your organization's account |
| Time: | Oct 12, 2017 10:22 AM (UTC) |

JsonCopy{
"event": "Account is running out of license",
"account_name": "OPSWAT IT",
"account_email": "it@opswat.com",
"devices_limit":1000,
"devices_monitored": 990,
"devices_left": 10,
"action_needed": "Please contact OPSWAT at https://www.opswat.com/contact in order to upgrade your organization's account",
"time": "Oct 02, 2017 10:39 AM (UTC)"
}
## [Device added](/docs/macloud-sdp/configuration---management/email-notifications#device-added)

Subject: [MetaDefender IT Access] Device added: LINCOLN7

| **Event:** | **Device added** |
| --- | --- |
| Nickname: | LINCOLN7-172911119 |
| Hostname: | LINCOLN7 |
| User: | alice |
| Device ID: | LINCOLN7 |
| User Identity: | N/A |
| MAC Address: | 19:03:f1:81:21:45 |
| Time: | Oct 09, 2017 09:38 AM (UTC) |

JsonCopy{
"event": "Device added",
"device_id": "deviceIDxxxx",
"nickname": "WSEVN02",
"hostname": "WSEVN02",
"group_name":"San Francisco",
"user_identity": "",
"agent_type": "Managed",
"time": "Sep 29, 2017 04:56 AM (UTC)",
"user": "username",
"network_info": [{
"ipv4": "109.184.237.115",
"ipv6": "fe80::2d88:eab7:6001:6ec7",
"mac": "02:21:9b:06:4b:96",
}]
}
## [Device uninstalled by a user](/docs/macloud-sdp/configuration---management/email-notifications#device-uninstalled-by-a-user)

Subject: [MetaDefender IT Access] Device uninstalled by user: LINCOLN8

HTML

| **Event:** | **Device uninstalled by user** |
| --- | --- |
| Nickname: | LINCOLN8-172911119 |
| Hostname: | LINCOLN8 |
| User: | username |
| Device ID: | LINCOLN8 |
| User Identity: | N/A |
| MAC Address: | 20:03:f1:81:21:45 |
| Time: | Oct 09, 2017 09:54 AM (UTC) |

JsonCopy{
"event": "Device uninstalled by user",
"device_id": "deviceIDxxxx",
"nickname": "WSEVN02",
"hostname": "WSEVN02",
"group_name":"San Francisco",
"user_identity": "",
"agent_type": "Managed",
"time": "Sep 29, 2017 04:56 AM (UTC)",
"user": "username",
"network_info": [{
"ipv4": "109.184.237.115",
"ipv6": "fe80::2d88:eab7:6001:6ec7",
"mac": "02:21:9b:06:4b:96",
}]
}
## [Device changed status to compliant](/docs/macloud-sdp/configuration---management/email-notifications#device-changed-status-to-compliant)

Subject: [MetaDefender IT Access] Changed status to compliant: LINCOLN8

| **Event:** | **Device changed status to compliant** |
| --- | --- |
| Nickname | <nick name> |
| Hostname | <host name |
| User | <user> |
| Details: | Device changed status to compliant |
| Cirical Issue | false/true |
| Device ID | <device id> |
| User Identity | <user identity> |
| Group Name | <group name> |
| MAC address | <mac address> |
| Time | <time> |

JsonCopy{
"event": "Changed status to compliant",
"device_id": "deviceIDxxxx",
"nickname": "WSEVN02",
"hostname": "WSEVN02",
"group_name":"San Francisco",
"user_identity": "",
"agent_type": "Managed",
"time": "Sep 29, 2017 04:56 AM (UTC)",
"issue": {
"total_issue": 10,
"total_critical_issue": 3,
"total_warning_issue": 7
},
"user": "username",
"network_info": [{
"ipv4": "109.184.237.115",
"ipv6": "fe80::2d88:eab7:6001:6ec7",
"mac": "02:21:9b:06:4b:96",
}],
"details": [
{
"category": "AV",
"products": [{
"id": "a896b7b839ef62671314990f8d1d6794",
"name": "Microsoft Security Essentials",
"vendor": "Microsoft Corp.",
"version": "4.4.0304.0",
"issues": ["Real time protection is on", "Virus definitions were updated within the last 3 days", "A full system scan was run within the last week", "35 threats detected within the last week"],
"critical": 1
}]
},
{
"category": "repeated_threats",
"total": 1,
"threats": [{
"critical": 0,
"file": "C:\\Windows\\KMSEmulator.exe",
"scan_time": "2015-05-12T23:32:19Z",
"threat_name": "@ApplicUnwnt.Win32/HackKMS.A",
"repeat": 2,
"product_name": "ESET Endpoint Security",
"product_vendor": "ESET",
"product_version": "5.0.2211.0",
"severity": "0",
"action": "5",
"type": "0"
 
}]
},
{
"category": "running_processes",
"total": 1,
"threats": [{
"critical": 0,
"file": "C:\\ProgramData\\WindowsMangerProtect\\ProtectWindowsManager.exe",
"hash": "e152e3ea7c356cfed40306ff946233d0",
"link":" https://www.metadefender.com/#!/results/file/ZTE3MDkwMXJrb0c5UWFYUFktSHlnYjVIMGot/regular/analysis",
"scan_time": "2015-05-13T17:00:34Z",
"threat_name": "Generic6.WQW",
"details": [{
"threat_name": "ADWARE/ELEX.Gen",
"av_name": "ClamAV"
}]
}]
},
{
"category": "ip_suspicious",
"total": 0,
"threats": []
}
]
}
## [Device reported threats](/docs/macloud-sdp/configuration---management/email-notifications#device-reported-threats)

Subject: [MetaDefender IT Access] Daily malware found: LINCOLN8

| **Event:** | **Daily malware found** |
| --- | --- |
| Nickname: | LINCOLN8 |
| Hostname: | LINCOLN8 |
| User: | username |
| Details: | Threat detected: Trojan.Win32.Heur.Gen ([View details on Metadefender Cloud](https://metadefender.opswat.com))Path: c:\program files\avast software\avast\avastsvc.exe Detected by: K7, CYREN, Emsisoft, K7, NANO Threat detected: Trojan222.Win32.Heur.Gen ([View details on Metadefender Cloud](https://metadefender.opswat.com))Path: c:\program files (x86) otepad++\plugins\poormanstsqlformatternppplugin\linqbridge.dll Detected by: CYREN, Emsisoft, K7, NANO, K7 |
| Critical Issue: | true |
| Device ID: | LINCOLN8 |
| User Identity: | N/A |
| MAC Address: | N/A |
| Time: | Oct 09, 2017 10:13 AM (UTC) |

JsonCopy{
"event": "Device infection found",
"device_id": "deviceIDxxxx",
"nickname": "WSEVN02",
"hostname": "WSEVN02",
"group_name":"San Francisco",
"user_identity": "",
"agent_type": "Managed",
"time": "Sep 29, 2017 04:56 AM (UTC)",
"issue": {
"total_issue": 10,
"total_critical_issue": 3,
"total_warning_issue": 7
},
"user": "tle",
"network_info": [{
"ipv4": "109.184.237.115",
"ipv6": "fe80::2d88:eab7:6001:6ec7",
"mac": "02:21:9b:06:4b:96",
}],
"details": [
{
"category": "repeated_threats",
"total": 1,
"threats": [{
"critical": 0,
"file": "C:\\Windows\\KMSEmulator.exe",
"scan_time": "2015-05-12T23:32:19Z",
"threat_name": "@ApplicUnwnt.Win32/HackKMS.A",
"repeat": 2,
"product_name": "ESET Endpoint Security",
"product_vendor": "ESET",
"product_version": "5.0.2211.0",
"severity": "0",
"action": "5",
"type": "0",
"existing": 1
}]
},
{
"category": "running_processes",
"total": 1,
"threats": [{
"critical": 0,
"file": "C:\\ProgramData\\WindowsMangerProtect\\ProtectWindowsManager.exe",
"hash": "e152e3ea7c356cfed40306ff946233d0",
"link":" https://www.metadefender.com/#!/results/file/ZTE3MDkwMXJrb0c5UWFYUFktSHlnYjVIMGot/regular/analysis",
"scan_time": "2015-05-13T17:00:34Z",
"threat_name": "Generic6.WQW",
"details": [{
"threat_name": "ADWARE/ELEX.Gen",
"av_name": "ClamAV"
}]
}]
},
{
"category": "ip_suspicious",
"total": 0,
"threats": []
}
]
}

<!-- source: https://www.opswat.com/docs/cm/configurations/endpoint-remediation-page -->

# Endpoint Remediation Page

My OPSWAT Central Management now empowers administrators to fully customize the remediation page with the organization's own brand and text for each device group individually. This powerful feature further enhances the end user experience to meet the strong demands of localization.

You can download a default rebranding package from My OPSWAT Central Management console and start customizing the logo and text in the package. Please make sure you follow the instructions below while you create a new rebranding package. My OPSWAT Central Management will not show a detailed error if you do not follow the below guideline today.

- **Don't alternate filenames** in the default package
- **Don't alternate field names** in all JSON file
- All JSON files must be **saved in UTF-8** format
- **Don't delete variables and html**, for example %product_name%, in JSON files
- The zip file should contain both logo.png and all JSON file **in the root folder**.

The screenshots and tables below show you how to customize color, text, and logo for each section on the remediation page.

![](https://uploads.developerhub.io/prod/97qW/pxlyr7g7txiukqasjhr8fsgm0iacgj6hu6z1vykjumuon1rk9y5f27bzlvrynz9r.PNG)

![](https://uploads.developerhub.io/prod/97qW/eoifxlhao0q9pqv6je3f7xg9rscjj4hp1o3ueea2zegr9a5a3ez98is2jncdghzt.jpg)

#### **Table 1: Remediation Page Sections**

Instructions to customize text, logo, and color for each section on the remediation page.

| Section | Description | File | Parameters need to be updated |
| ---- | ---- | ---- | ---- |
| 1 | Page title | generic.json | *page_title* |
| 2 | Logo | logo.png | Replace the logo.png file in the rebranding package with your organization logo. |
| 3 | Overall Device Status | overall_status_guideline.json *generic.json* | Text of the overall status bar is defined in the parameter *<remediation_code>.sub_title* in the file *overall_status_guideline.json*, for example: *com_100.sub_title.* See the detailed explanation for each status code in Table 3. Color of the overall status bar is defined in the file *generic.json*. See the detailed explanation for color code in Table 2. |
| 4 | Issues found | generic.json | Text of this section is defined in the parameter *issues.found_text* |
| 5 | Issue classification | generic.json | *required_text:* tells users that they MUST fix issues under this section to keep their device compliant. *recommended text*: tells users that issues under this section are recommended and won't impact to device compliant status. |
| 6 | Issue summary | category_<category name on the policy>.json | *<issue>.summary* For example: *av_001.summary*. See the detailed explanation for each issue code in the Table 4 - Table 20. |
| 7 | Issue explanation | category_<category on the policy>.json | The parameter *<issue>.detail,* for example: *av_002.detail,* tells users a summary on what went wrong on a device for each category. Additional to that, variables in the _<issue>.detail, if any,_will be replaced as below: - %issue_text% (detailed issue) is replaced with the parameter *issue_details.<issue code>.issue_text*. - %issue_guide% (remediation guideline) is replaced with the parameter *issue_details.<issue code>.issue_guide*. - %product_name% will be replaced with installed applications/approved applications' name if configured. See the detailed explanation for each issue code in the Table 4 - Table 20. |
| 8 | Overall guideline | overall_status_guideline.json | A message you would like to guide your users based on each overall device status is defined in *<remediation_code>.description* For example: com_100.description See the detailed explanation for each remediation code in the Table 3. |
| 9 | Device information | generic.json | Show device information. If a parameter in this block is set as blank (""), that information will not be shown. And if all device information parameters are set as blank (""), entire Device Information block will be hidden. *device_text:* shows device information block *device_info.hostname*: a device's hostname. device_info.managed: account name that a device is connecting to. *device_info.device_id*: a device ID ID. *device_info.last_report*: Last time a device reported data to servers. *device_info.device_username*: Username of the last active user. *device_info.device_nickname*: Device Nick Name. |
| 10 | Contact Administrator | generic.json | A message to guide your users on how to contact your helpdesk/administrators when your users need help. *contact.text*: text you want to show for that block. contact.type: if you want to show the Contact Administrator block to your users. Its value should be: - 0: hides the Contact Administrator block - 1: show it as a hyperlink and redirects a user to a page defined in *contact.detail* - 2: send an email to an email address defined in *contact.detail* when a user clicks on it. In this case, you can define a message (*contact_it* parameters) to users  after the system sends an email to the defined email. - 3: show a text block when a user clicks on it. The message inside the block is defined in *contact.detail*. |
| 11 | Temporary Access | generic.json | Only applicable if a device is granted temporary access to protected apps. Those apps will be shown on the remediation page like the above sample screenshot. *temporary_access_text*: a message to tell users that they are granted temporary access to protected apps. See item #16 in this table to customize time units. |
| 12 | Font | generic.json | *font_name*: specify what font family is used on the remediation page. Only support a device's system font families, for example: Arial, Helvetica, Times New Roman, Times, Courier New, Courier. The *font_name* can hold several font names as a "fallback" system. If the browser does not support the first font, it tries the next font. If there is no supported font or its value is empty, the remediation page will use the MetaDefender IT Access's default font "SimplonNorm, Arial ,sans-serif;" For example: "*customization.font_name":"" "customization.font__name": "Arial" "customization.font_name*": "Arial, Helvetica, sans-serif" |
| 13 | Custom Check | content.json | customcheck_output_  :message: Only applicable if the custom check feature is enabled. Admins can set this value to expose an custom script output message to end-users on remediation pages. If a script returns FALSE not empty, the custom script output message will be exposed after this field value. If empty, the custom script output message will not be shown. The default value is empty. |
| 15 | Indicate what issues should be shown on the page | generic.json | *show_issues_with_severity*: shows issues that match the severity and above to users. For example "warning": show issues with Warning severity and above "critical": show issues with Critical severity and above. |
| 16 | Time Units | generic.json | *time* object |

#### **Table 2: Color Guideline**

Define colors you would like to use on the remediation page.

File: generic.json.

| Color Parameter | Description |
| ---- | ---- |
| colors.no_issue | It is used for the overall status bar when a device is compliant and has no issues based on a policy. |
| colors.recommended_issue | This is used for the overall status bar when a device is compliant and has only recommended issues. It's also used for a Recommended issue's bar |
| colors.required_issues | This is used for the overall status bar when a device is non-compliant OR has any required issues It's also used for a Required issue's bar |
| colors.text_primary | text color |
| colors.issue_background | background color of issue box |
| colors.header_hover | color of an issue bar when a user hovers on it. |

**Table 3: Overall device status**

Define a device's overall status.

File: overall_status_ guideline.json

| Remediation Code | Conditions to show the message |
| ---- | ---- |
| com_100 | - Secure Access is enabled. - A user gets blocked from accessing a protected app via IdP - A device has issues. |
| com_101 | - Secure Access is enabled. - A user gets blocked from accessing a protected app via IdP - A device has no issues. This happens when an admin configures a compliant rule with a sensitive threshold greater than 1 to consider a device as compliant. |
| com_202 | - Device has issues. |
| com_203 | - Device has no issues. - Device status is compliant |
| com_204 | - Secure Access is enable. - Device has no issues and non-compliant. This happens when an admin configures a compliant rule with a sensitive threshold greater than 1 to consider a device as compliant. |
| com_205 | - Secure Access is disable. - Device has no issues and non-compliant. This happens when an admin configures a compliant rule with a sensitive threshold greater than 1 to consider a device as compliant. |
| com_300 | - Secure Access is enable. - Device has no issues. - Device is granted temporary access to at least one protected app. Note: The remediation page is shown to remind users how long they can temporary access to protected apps. |
| com_301 | - Secure Access is enable. - Device has issues. - Device is granted temporary access to at least one protected app. Note: The remediation page is shown to remind users how long they can temporary access to protected apps. |

**Table 4: Vulnerabilities and Exposures Issues**

Define issue summary and explanation for policy checks in Vulnerabilities and Exposures category.

File: category_vulnerability.json

| Parameter | Explanation |
| ---- | ---- |
| ve_01 | Device has issues with Vulnerabilities and Exposures checks. The %resolution% variable in ve_01.detail will be replaced by the *remediation_guideline.issue_text* parameter. |
| remediation_guideline | Remediation guideline. - up_to_latest: when an application requires an update to its latest version. - up_higher_or_equal: when an application requires an update to a version higher than or equal to a required version. - up_higher_than: when an application requires an update to a version higher than a required version. |

**Table 5: Patch Management Issues**

Define issue summary and explanation for policy checks in Patch Management category.

File: category_patch_management.json

| Parameter | Explanation |
| ---- | ---- |
| pm_001 | No patch management application installed. |
| pm_002 | At least one patch management application is installed but all of them has issues. Issue codes: - vl_01: when a device doesn't turn on auto-update on any installed patch management agents. - other codes: when a device has not installed required missing patches. |

**Table 6: Anti-malware Issues**

Define issue summary and explanation for policy checks in Anti-malware category.

File: category_antimalware.json

| Parameter | Explanation |
| ---- | ---- |
| av_001 | No approved anti-malware products are installed. |
| av_002 | At least one approved anti-malware product is installed but all of them has issues. Issue codes: - av_02: RTP is not enable. - av_031: virus definition is out of date. - av_032: a device has not updated the virus definition. - av_041: a device has never ran any full scan. - av_042: a device has not ran any full scan in last N days (N is a number of days that is configured on a policy). - av_05: local anti-malware detected threats in the last N days (N is a number of days that is configured on a policy). |

**Table 7: Encryption Issues**

Define issue summary and explanation for policy checks in Encryption category.

File: category_encryption.json

| Parameter | Explanation |
| ---- | ---- |
| ec_001 | No approved encryption products are installed. |
| ec_002 | At least one approved encryption product is installed but all of them has issues. Issue codes: - ec_031: MetaDefender Endpoint does not support to check encryption state of the product. - other codes: encryption state of a volume/partition. |

**Table 8: User Authentication Issues**

Define issue summary and explanation for policy checks in User Authentication category.

File: category_user_authentication.json

| Parameter | Explanation |
| ---- | ---- |
| ua_001 | A device has an issue within this category. Issue codes: - ua_01: User password protection is disabled. - ua_021: MetaDefender Endpoint doesn't support to check lock screen timeout on a operating system. - ua_022:  Lock screen timeout is not set. - ua_023: Lock screen timeout is over N minutes. (N is a number of minutes that is configured on a policy). |

**Table 9: Anti-phishing Issues**

Define issue summary and explanation for policy checks in Anti-phishing category.

File: category_antiphishing.json

| Parameter | Explanation |
| ---- | ---- |
| af_001 | A device has issues in this category. |

**Table 10: Backup Issues**

Define issue summary and explanation for policy checks in Backup category.

File: category_backup.json

| code | Case |
| ---- | ---- |
| bk_001 | No backup applications are installed. |
| bk_002 | Device has not run backups recently. |

**Table 11: Firewall Issues**

Define issue summary and explanation for policy checks in Firewall category.

File: category_firewall.json

| Parameter | Explanation |
| ---- | ---- |
| fw_001 | A device has issues in this category. |

**Table 12: Hard Drive Issues**

Define issue summary and explanation for policy checks in Hard Drive category.

File: category_storage.json

| Parameter | Explanation |
| ---- | ---- |
| hr_001 | A device has issues in this category. |

**Table 13: Operating System Issues**

Define issue summary and explanation for policy checks in Operating System category.

File: category_os.json

| Parameter | Explanation |
| ---- | ---- |
| os_001 | Operating system version on a device is not approved. Variables in the *os_001.detail* will be replaced with parameters in the *os_001.issue_details*. |
| os_003 | Device has not rebooted for a long time. |

**Table 13: Custom Check Issues**

Define issue summary and explanation for policy checks in Custom Check category.

File: category_custom_check.json

| Parameter | Explanation |
| ---- | ---- |
| gc_001 | A device failed a custom check. |

**Table 14: Threats detected by Multiscanning technology Issues**

Define issue summary and explanation for policy checks in Threats detected by Multiscanning technology category.

File: category_multiscanning.json

| Parameter | Explanation |
| ---- | ---- |
| ip_001 | MetaDefender Endpoint detected threats on a device. |

**Table 15: Repeated Threats Issues**

Define issue summary and explanation for policy checks in Repeated threats category.

File: category_repeated_threats.json

| Parameter | Explanation |
| ---- | ---- |
| ir_001 | Local anti-malware detected threats on a device. ir_001.action_x: what action the local anti-malware took when it detected a specific threat, in which x = 0..5 or default. |

**Table 16: Unwanted Applications Issues**

Define issue summary and explanation for policy checks in Unwanted Applications category.

File: category_unapproved_apps.json

| Parameter | Explanation |
| ---- | ---- |
| ua_001 | A device installed at least unapproved applications. |

**Table 17: Security & Health Issues**

Define issue summary and explanation for policy checks in Security & Health category on mobile devices.

File: category_mobile.json

| Parameter | Explanation |
| ---- | ---- |
| sh_001 | Device does not have screen lock and passcode. |
| sh_002 | Device is jailbroken. |
| sh_003 | Device is rooted. |
| sh_004 | Device's internal storage is not encrypted. |
| sh_005 | Device is running an out-of-date operating system version. |

**Table 18: Suspicious IP Connections Issues**

Define issue summary and explanation for policy checks in Suspicious IP Connections category on mobile devices.

File: category___suspicious_connection.json

| Parameter | Explanation |
| ---- | ---- |
| ic_001 | Device is connecting to a suspicious website/server. |

**Table 19: Issues based on compliance rules**

Define issue summary and explanation if a device doesn't meet compliance rules.

File: rule_policy.json

| Parameter | Explanation |
| ---- | ---- |
| ag_002 | Device has not reported compliance data yet/has not been checked in last X hours. |
| ag_003 | MetaDefender Endpoint version on a device is not approved. |
| dr_002 | Device is non-compliant because it doesn't meet any compliant rules in a policy. |
| dt_001 | Device type is not approved. Variable %device_type% will be replaced with parameter *dt_001.vm/dt_001.desktop/dt_001.laptop/dt_001.server*. |

**Table 20: Issues based on access rules**

Define issue summary and explanation if a device doesn't meet access rules. *

**This is only applicable if you enable Secure Access and these issues are only shown when a user gets blocked from accessing a protected app via IdP.*

File: rule_secure_access.json

| Parameter | Explanation |
| ---- | ---- |
| ag_001 | MetaDefender Endpoint is not detected on a device. Variable %os__name%_ in the *ag_001.detail* will be replaced with the parameter *for_windows_7* or *for mac* in the generic.json file. |
| ag_004 | MetaDefender Endpoint on the device is reporting to another account. Variable %os__name%*in the **ag_004.detail** will be replaced with the parameter **for_windows_7** or **for mac** in the generic.json file.* _ |
| ag_005 | MetaDefender Endpoint on the device is disconnected. This may happen when your account enables Lost Device settings to recycle license of disconnected devices. |
| ag_006 | MetaDefender Endpoint on the device could not enroll to your account due to license limit. |
| gp_001 | Device belongs to a specific group in an access rule. |
| ap_001 | Device attempts to access a protected application that is not allowed based on an access rule. |
| dr_001 | Device doesn't meet any other access rules. |
| dr_003 | Operating system of a device is blocked by the operating system access rule. |
| cf_003 | A certificate of a protected app's IdP is expired or invalid. |

<!-- source: https://www.opswat.com/docs/cm/endpoint-security-solution/metadefender-endpoint-policies -->

# MetaDefender Endpoint Policies

My OPSWAT Central Management offers well beyond basic compliance checks to ensure with the highest degree of confidence that your endpoints are secure. In addition to standard compliance checks such as OS level, Security Software installed and configured correctly, Encryption, Password and Firewall settings, My OPSWAT Central Management has functionality to check for vulnerability and patch management, manage potentially unwanted applications, multi-engine anti-malware scanning, removable media protection, anti-keylogger and screen capture protection. My OPSWAT Central Management provides the most comprehensive check in the industry.

## Settings

Define actions you would like the client performs on devices

- Advanced Malware Detection: protect your devices from risky removable media and schedule a malware scan on devices. [Learn more](https://www.opswat.com/docs/cm/knowledge-base/what-is-threat-detection-on-my-opswat-central-management)

![](https://uploads.developerhub.io/prod/97qW/0k5ua11yq6vhwqlxgjq5x8x01dxuwqm170pxqvhxi22royrz2500dszw0sj0xm8s.png)

## Monitoring issues on devices

Note: even you don't enable a category on a policy, MetaDefender Endpoint still collects all information related to that category today

You can define how to consider an issue and severity of each issue on devices for Vulnerabilities, Compliance, Unwanted Applications, Malware Detection. You can also select the device types (Desktops, laptops, Virtual Machines, and Servers) these policies are applied to as well as by Operating System type (Windows, macOS, Linux, Android, and iOS)

![](https://uploads.developerhub.io/prod/97qW/21p399mhps10akqyoobgr1pn44mxneh63pz7xjg0zp7iipchb77olxnx4ft75sbh.png)

## Configuring device compliance status based on facts

Click on the **Rules** to define rules for device status based on device issues and other conditions.

- You can edit existing device status rules
- OR Add/Remove device status rules. Note that you cannot delete the default rule. It's a fallback rule in case a device doesn't meet any rules you define.

![](https://uploads.developerhub.io/prod/97qW/s65mzxd0hprsks95gen5ew1o5dejkpbzttd58hyg302gwfoh1ra2pfn8e7xctkaf.png)

***Notes:***

- My OPSWAT Central Management processes rules by order. If a device meets a rule (must to meet all conditions defined in that rule), it will get device status in that rule.

**For example:** a policy has 4 rules below:

![](https://uploads.developerhub.io/prod/97qW/626nfpbdui63f5ryaxzpgixkz1mm5u7jkl78tvgvyy8xy0zhl72grkebxgor9ff0.png)

**Case 1:** my device reported with no issues and has not checked in 25 hours.

Device status: the device is considered as non-compliant with Rule #1

**Case 2:** my device reported with no issue 5 minutes ago

Device status: the device is considered as compliant with Rule #2

## Configuring grace period for specific controls and categories

Click on the **Rules** to add device status rules and configure grace period for specific controls and categories.

- You can adjust the policy rule by setting the time of consecutive reports
- Select specifics for categories that are allowed grace period

![](https://uploads.developerhub.io/prod/97qW/a0os4x0o2etgvcsal8vz6oij95wlnb1nh66j5kqk5nac8j4kjf54pthfra02phkz.png)

***Notes:***

- This configuration is only available now for "Vulnerability and Exposures" category.
- When configured, the device will be in the grace period of the set time. This allows the user the given time to resolve the issue before the device becomes non-compliant. During this period, a warning message will be displayed on the remediation page.

![](https://uploads.developerhub.io/prod/97qW/9f5foeejd73xy9bk6toye5rbhbpnc31om5ex2rctgajxcp6sh0s5n8i7ahi90h57.png)

**Case 1:** the administrator configures vulnerabilities and exposures for the devices and its criticality when OPSWAT score is great than or equal to 8.

![](https://uploads.developerhub.io/prod/97qW/80pmnfbdt4pz6w3qo7mia3hc1w2rsbdu6dlspqbs2xlig8q48rgja8dleif35m26.png)

Device status: the device is considered as non-compliant after the set time in Vulnerabilities and Exposures categories

![](https://uploads.developerhub.io/prod/97qW/v46towcfsnvz8sdxdyzobxygl8hu9nfl7t15vj375qnk5p4oxf792hpk7y4fzuad.png)

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)

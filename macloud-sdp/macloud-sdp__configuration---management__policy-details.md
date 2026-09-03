<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/policy-details -->

# Policy Details

MetaDefender IT Access offers well beyond basic compliance checks to ensure with the highest degree of confidence that your endpoints are secure. In addition to standard compliance checks such as OS level, Security Software installed and configured correctly, Encryption, Password and Firewall settings, MetaDefender IT Access has functionality to check for vulnerability and patch management, manage potentially unwanted applications, multi-engine anti-malware scanning, removable media protection, anti-keylogger and screen capture protection. MetaDefender IT Access provides the most comprehensive check in the industry.

## [Settings](/docs/macloud-sdp/configuration---management/policy-details#settings)

Define actions you would like the client performs on devices

- Advanced Malware Detection: protect your devices from risky removable media and schedule a malware scan on devices. [Learn more](/docs/macloud-sdp/kb/what-is-threat-detection-on-metaaccess-)

## [Monitoring issues on devices](/docs/macloud-sdp/configuration---management/policy-details#monitoring-issues-on-devices)

Note: even you don't enable a category on a policy, MetaDefender Endpoint still collects all information related to that category today

You can define how to consider an issue and severity of each issue on devices for Vulnerabilities, Compliance, Unwanted Applications, Malware Detection. You can also select the device types (Desktops, laptops, Virtual Machines, and Servers) these policies are applied to as well as by Operating System type (Windows, macOS, Linux, Android, and iOS)

## [Configuring device compliance status based on facts](/docs/macloud-sdp/configuration---management/policy-details#configuring-device-compliance-status-based-on-facts)

Click on the **Rules** to define rules for device status based on device issues and other conditions.

- You can edit existing device status rules
- OR Add/Remove device status rules. Note that you cannot delete the default rule. It's a fallback rule in case a device doesn't meet any rules you define.

***Notes:***

- MetaDefender IT Access processes rules by order. If a device meets a rule (must to meet all conditions defined in that rule), it will get device status in that rule.

**For example:** a policy has 4 rules below:

**Case 1:** my device reported with no issues and has not checked in 25 hours.

Device status: the device is considered as non-compliant with Rule #1

**Case 2:** my device reported with no issue 5 minutes ago

Device status: the device is considered as compliant with Rule #2

## [Configuring grace period for specific controls and categories](/docs/macloud-sdp/configuration---management/policy-details#configuring-grace-period-for-specific-controls-and-categories)

Click on the **Rules** to add device status rules and configure grace period for specific controls and categories.

- You can adjust the policy rule by setting the time of consecutive reports
- Select specifics for categories that are allowed grace period

***Notes:***

- This configuration is only available now for "Vulnerability and Exposures" category.
- When configured, the device will be in the grace period of the set time. This allows the user the given time to resolve the issue before the device becomes non-compliant. During this period, a warning message will be displayed on the remediation page.

**Case 1:** the administrator configures vulnerabilities and exposures for the devices and its criticality when OPSWAT score is great than or equal to 8.

Device status: the device is considered as non-compliant after the set time in Vulnerabilities and Exposures categories

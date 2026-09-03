<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/what-antivirus-products-are-supported-by-nac -->

# What Antivirus products are supported by NAC?

This article applies to the current NAC Enforcer, Web UI, and the latest NAC Policy Key installed on Windows or macOS systems.

This article lists all antivirus products and vendors currently supported by OPSWAT’s MetaDefender NAC.

Such support comprises the following functions:

- These policies are evaluated in the order of (1) **Installed,** then (2) **Running**, then (3) **Definitions**.
- If a Policy Key does not show an antivirus as **Running**, it can not yet evaluate whether **Definitions** are up to date, etc.

| Windows | macOS |
| --- | --- |
| - Authentium - Avast - AVG - AVGuard - Avira - Bitdefender - CarbonBlack - Comodo - CrowdStrike - Cylance - ESET (NOD32) - EZ Antivirus - Faronics - Fortinet - FSecure Antivirus - Gdata - Immunet - iolo System Shields - Ivanti - Kaspersky - Landesk - LightSpeed - Malwarebytes Antivirus - McAfee - McAfee NA - McAfee 45 - Microsoft Security Products. Microsoft has released a variety of antivirus products, including:    - Defender (Windows 8, 8.1 and 10)   - SCEP   - Security Essentials   - OneCare - Panda - PCtools - SecureIT - SentinelOne - Sophos - Sophos X - WebRoot (SpySweeper) - Symantec Personal - Symantec Enterprise - Norton - TrendMicro - TrendMicro Corp - Vipre Antivirus - ZoneAlarm | - Avast - Avira - AVG - BitDefender - ClamXav - Comodo - CrowdStrike - Cylance - ESET - iAntiVirus - Intego - Kaspersky - MacKeeper - McAfee - Microsoft SCEP - Norton - Panda - Sophos - Sophos X - SentinelOne - TrendMicro - Webroot |

## [Policy Key endpoint web-responsive messages](/docs/manac/nac-v8.1.1/knowledge-base/what-antivirus-products-are-supported-by-nac#policy-key-endpoint-web-responsive-messages)

### [Antivirus Not Installed](/docs/manac/nac-v8.1.1/knowledge-base/what-antivirus-products-are-supported-by-nac#antivirus-not-installed)

- This page will be displayed on endpoints that have the NAC Policy Key running but are quarantined for not having an antivirus product installed.
- Popular antivirus vendor websites are listed, and blocked clients will have direct access to those websites via the message page, so that they can download a suitable, supported product and thus remediate their non-compliant state.

### [Antivirus Definitions Out-Of-Date/Antivirus Is Not Running](/docs/manac/nac-v8.1.1/knowledge-base/what-antivirus-products-are-supported-by-nac#antivirus-definitions-out-of-dateantivirus-is-not-running)

This message will allow blocked clients to access vendor-specific resources, based on the vendor product detected on their endpoint device.

The **Vendor Resources** link in the example above points to the ESET website.

Support:

For queries, concerns or issues regarding **NAC’s Supported Antivirus Products**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

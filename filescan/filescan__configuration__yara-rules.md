<!-- source: https://www.opswat.com/docs/filescan/configuration/yara-rules -->

# YARA Rules

The Sandbox engine contains a set of YARA rules in the `/home/sandbox/sandbox/transform/yara/rules` folder.

If Sandbox is connected to the Internet, these built-in YARA rules are periodically updated from a GitHub repository (<https://github.com/filescanio/fsYara>) maintained by OPSWAT Malware Analysts. After an update, the engine recompiles the `master_file.yarc` file that contains all rules in a compiled form. This is crucial for efficient YARA matching.

It is also possible to add custom YARA rules as `.yar` files in the `/home/sandbox/sandbox/transform/yara/rules/custom` folder, but it is necessary to modify the YARA update configuration to always generate `master_file.yarc` on Sandbox startup:

**Step #1 - Open** `/home/sandbox/sandbox/transform.cfg` **in a text editor**

**Step #2 - Modify the configuration by adding the following property:**

transform.cfgCopyrunYaraUpdateOnStartup=true

**Step #3 - Save the file and restart the** `sandbox` **service**

## [Property details](/docs/filescan/configuration/yara-rules#property-details)

| Property Name | Default Value | Description |
| --- | --- | --- |
| runYaraUpdateOnStartup | false | Main switch to enable / disable YARA updates on Sandbox startup |
| yaraDefaultStrengthPreferScoreValueIfPresent | true | Prefer using `score` metadata when it is available, instead of relying on other heuristic methods |

## [Adding custom YARA rules](/docs/filescan/configuration/yara-rules#adding-custom-yara-rules)

After this change, custom `.yar` files can be copied to the `/home/sandbox/sandbox/transform/yara/rules/custom` folder, and these YARA rules will be automatically loaded by the Sandbox engine.

To explicitly control the verdict of your custom YARA rule, make sure to include a `score` field in the rule’s metadata. The sandbox engine will automatically extract this field and use it as the primary factor when mapping the YARA rule’s verdict. For example:

yaraCopyrule Example_Malicious_Rule
{
meta:
description = "Detects malicious behavior"
author = "Your Name"
score = 75
strings:
$str = "suspicious_string"
condition:
$str
}
### [Verdict mapping](/docs/filescan/configuration/yara-rules#verdict-mapping)

| YARA Metadata | Severity Level | Verdict |
| --- | --- | --- |
| score = 0 | NO_IMPACT | NO_THREAT |
| score = 10 | VERY_LOW_IMPACT | LOW_RISK |
| score = 25 | LOW_IMPACT | LOW_RISK |
| score = 50 | CONSIDERABLE_IMPACT | LOW_RISK |
| score = 75 | SEVERE_IMPACT | HIGH_RISK |
| score = 100 | CRITICAL_IMPACT | CONFIRMED_THREAT |

After adding or modifying a custom rule, please always **restart** the `sandbox` service!

Warning

All custom changes made in the `/home/sandbox/sandbox/transform/yara/rules` folder **will be lost** during a Sandbox installation!

If you add any custom YARA rules here, please remember to save them and **restore them after upgrading Sandbox!**

## [Additional Community YARA rules](/docs/filescan/configuration/yara-rules#additional-community-yara-rules)

If the `Sandbox_UseCommunityYaraRules` option is set to `true` in the `install.cfg` file (see [Installation Options](/docs/filescan/installation/installation-options)), then the Sandbox installer will clone the following GitHub repositories containing the latest YARA rules provided by the Malware Analysis community (these repositories are not controlled by OPSWAT):

| List of Community YARA Repositories |
| --- |
| <https://github.com/Yara-Rules/rules> |
| <https://github.com/Neo23x0/signature-base> |
| <https://github.com/advanced-threat-research/Yara-Rules> |
| <https://github.com/StrangerealIntel/DailyIOC> |
| <https://github.com/AlienVault-Labs/AlienVaultLabs> |
| <https://github.com/ditekshen/detection> |
| <https://github.com/reversinglabs/reversinglabs-yara-rules> |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

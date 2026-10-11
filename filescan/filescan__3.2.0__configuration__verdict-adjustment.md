<!-- source: https://www.opswat.com/docs/filescan/3.2.0/configuration/verdict-adjustment -->

# Verdict Adjustment

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Step #1 - Open** `/home/sandbox/sandbox/transform.cfg` **in a text editor**

**Step #3 - Save the file and restart the** `sandbox` **service**

## [**Disable Threat indicators**](/docs/filescan/3.2.0/configuration/verdict-adjustment#disable-threat-indicators)

One or more Threat indicators can be disabled, so those will not be evaluated during the verdict calculation process.

transform.cfgCopyignoreVerdictForMatchingConsumerIDs=A000,AIT001

| Property name | Default value | Description |
| --- | --- | --- |
| ignoreVerdictForMatchingConsumerIDs |  | IDs to disable, separated by comma |

## [**Escalate Threat indicators**](/docs/filescan/3.2.0/configuration/verdict-adjustment#escalate-threat-indicators)

One or more Threat indicators can be escalated, so those will be evaluated as Malicious during the verdict calculation process.

transform.cfgCopyescalateVerdictToMaliciousForMatchingConsumerIDs=A000,AIT001

| Property name | Default value | Description |
| --- | --- | --- |
| escalateVerdictToMaliciousForMatchingConsumerIDs |  | IDs to escalate, separated by comma |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

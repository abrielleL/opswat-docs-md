<!-- source: https://www.opswat.com/docs/filescan/configuration/llm-scanning -->

# LLM Scanning

View as Markdown Ask ChatGPT about this page Ask Claude about this page

A threat can be baked into the model artifact before it ships, or it can live in how the model responds once deployed. LLM Scanner covers both, through two complementary detection capabilities.

| **Feature** | **Description** |
| --- | --- |
| **LLM Static Analysis** | Malicious payloads and arbitrary code-execution paths can hide inside model files. The scanner detects the correct format, then parses it down to its structure to surface embedded payloads, dangerous imports, and anomalous signatures. |
| **LLM Dynamic Analysis** | Even a clean model file is no guarantee of safe behavior. The scanner evaluates the deployed model's behaviors itself, dynamically probing it with adversarial prompts to expose prompt injection, sensitive-data disclosure, and other weaknesses that only appear at inference time. |

**Step #1 - Open** `/home/sandbox/sandbox/transform.cfg` **in a text editor**

**Step #2 - Modify the configuration by adding the following property:**

transform.cfgCopyrunStaticLLMScan=true
runDynamicLLMScan=true
dynamicLLMScanHarnessAddress=<Harness address>
dynamicLLMScanHarnessApiKey=<Harness API key>
dynamicLLMScanTimeout=3600

**Step #3 - Save the file and restart the** `sandbox` **service**

## [Property details](/docs/filescan/configuration/llm-scanning#property-details)

| Property Name | Default Value | Description |
| --- | --- | --- |
| runStaticLLMScan | true | Switch to enable / disable static LLM scanning |
| runDynamicLLMScan | true | Switch to enable / disable dynamic LLM scanning |
| dynamicLLMScanHarnessAddress | empty | Address of the harness where the scanned model is loaded |
| dynamicLLMScanHarnessApiKey | empty | API key of the harness where the scanned model is loaded |
| dynamicLLMScanTimeout | 3600 | Maximum timeout of the dynamic LLM scanning in seconds. Value range: 30 - 18000 |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

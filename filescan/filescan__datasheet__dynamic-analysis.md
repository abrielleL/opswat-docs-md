<!-- source: https://www.opswat.com/docs/filescan/datasheet/dynamic-analysis -->

# LLM Dynamic Analysis

View as Markdown Ask ChatGPT about this page Ask Claude about this page

A model file itself can be legit, but that isn't the end. The risk isn't only what's stored on disk, it can be how the model responds once it's running. A prompt drafted to be malicious on purpose, trying to leak the system prompt, give a malicious instruction, or hand back an attacker's payload, can turn a legit model into a bad weapon.

MetaDefender Aether's LLM Scanner evaluates the deployed model's behavior itself dynamically by sending adversarial prompts to a live endpoint and judging the responses, to expose the behavioral weaknesses that only appear when the model runs. We cover all the AI threat vectors defined in OWASP Top 10 for LLM Applications - a standard framework for AI threat.

### Key Capabilities

- **Adversarial Prompt Technique Suite:** Evaluates the live model with **50+ techniques** and **1000+ adversarial prompts** spanning the OWASP LLM Top 10 risk categories.
- **Automated Response Judging:** Multiple judges mechanisms to score each response for signs the model was influenced.

- **Two-Axis Verdicts:** Separates how confident a finding is from how damaging it would be, so results are easy to triage.
- **OpenAI-Compatible Endpoint Testing:** Connects to any model that exposes an OpenAI-style chat-completions API, so it works against local and hosted deployments alike.

## Supported Model-Behavior Threat Vectors

### Prompt Injection

Crafted inputs override the model's instructions, making it ignore its guardrails and follow the attacker instead.

| **Techniques** | **Description** |
| --- | --- |
| Direct Prompt Injection | Instructions written straight into the user channel to override the model's instruction hierarchy. |
| Indirect Prompt Injection | Attacker instructions embedded in third-party content the model ingests as data. |
| Jailbreak & Safety Bypass | Inputs that make the model disregard its own safety policy: refusal suppression, prefix injection, adversarial suffixes, format coercion. |
| *And more than 10 other techniques* |  |

### Sensitive Information Disclosure

The model reveals private data it should keep to itself, training data, credentials, or other secrets.

| **Techniques** | **Description** |
| --- | --- |
| Credential Leak in Output | API keys, tokens, passwords, or session material appearing in a response. |
| PII Exposure in Output | Personal data the assistant holds (an SSN, a phone number) surfaced to an unverified caller. |
| Sensitive Document Disclosure | A held document such as audit, legal, HR, or medical is disclosed or reformatted for an unauthorized recipient. |
| *And more than 10 other techniques* |  |

### Supply Chain

A compromised base model, adapter, or dependency carries risk into the deployed model's behavior.

| **Techniques** | **Description** |
| --- | --- |
| AI Supply Chain Compromise | Compromise of the models, datasets, packages, plugins, or MCP servers an AI system assembles from. |
| Hallucinated Dependency Exploitation | Registering package names a model tends to hallucinate, so later generations resolve to attacker artifacts. |
| Tool and Context Poisoning | Injection carried at the tool or protocol layer, a poisoned tool description, schema, or returned output. |
| *And more than 5 other techniques* |  |

### Data and Model Poisoning

Manipulated training or fine-tuning data plants hidden behavior or bias that surfaces on certain inputs.

| **Techniques** | **Description** |
| --- | --- |
| Retrieval / RAG Poisoning | Whether the model writes a knowledge-base document that reads as a standing instruction to a future assistant. |
| Persistent Memory Poisoning | Whether the model saves a memory note that overrides its own future behavior or silently captures user data. |
| Training & Fine-tuning Data Poisoning | Whether a fabricated training-data citation or forged transcript planted in context biases the next reply. |

### Improper Output Handling

Unsafe content in the model's output, scripts, markup, or commands that harms the systems consuming it.

| **Techniques** | **Description** |
| --- | --- |
| Unexpected Code Execution | Whether the model writes a knowledge-base document that reads as a standing instruction to a future assistant. |
| Malware and Exploit Code Generation | Whether a fabricated training-data citation or forged transcript planted in context biases the next reply. |
| Harmful Content Generation | Actionable illegal, violent, or abusive content, including step-by-step operational guidance for real-world harm. |
| *And more than 10 other techniques* |  |

### Excessive Agency

The model takes actions or calls tools beyond what it should, given too much autonomy or permission.

| **Techniques** | **Description** |
| --- | --- |
| Agentic Tool Misuse | Prompts that steer an agent into tool calls or actions beyond the intended scope of its task. |

### System Prompt Leakage

The model discloses its hidden system prompt, exposing the instructions, rules, or secrets embedded there.

| **Techniques** | **Description** |
| --- | --- |
| System Prompt Leak | The configuration a model was given, reproduced, paraphrased, or reconstructed in its output. |
| Guardrail and Reasoning Disclosure | The model reveals its safety rules, filter logic, or hidden reasoning a map for bypassing them. |

### Misinformation

Confident but false or fabricated output that a user could act on as if it were true.

| **Techniques** | **Description** |
| --- | --- |
| Disinformation Generation at Scale | Mass-producing coherent false narratives, fake sources, or synthetic personas for influence operations. |
| Fraud and Social Engineering Content | Crafting phishing, pretexting, BEC, or scam material, including deepfake-assisted lures. |
| Malicious Workflow Automation | Orchestrating a criminal campaign end to end through generation, targeting, distribution, and iteration. |

### Unbounded Consumption

Inputs that push the model into runaway resource use, a denial-of-service or denial-of-wallet risk.

| **Techniques** | **Description** |
| --- | --- |
| Unbounded Consumption & Cost Abuse | A request engineered so the only way to satisfy it is to generate far more output than any bounded answer needs, burning tokens, latency, and cost. |

### Showcase Report

Prompt injection stands out as one of the most prevalent threats facing large language models in the wild. This technique is notorious for its ability to override a model's own instructions, leak its system prompt, or carry out an attacker's commands instead of the user's. Its simplicity and endless variations make it a significant threat, causing data exposure, misuse, and reputational damage for both individuals and businesses. Detecting whether a model is susceptible is of paramount importance, as it unveils critical details about how the model behaves under adversarial pressure, which give way, and where an attacker could seize control. This intelligence enables cybersecurity experts to harden the model, apply targeted defenses, additional guardrails, and decide with confidence whether it is safe to deploy.

Let's see how the LLM Scanner evaluate a model's behavior with a crafted adversarial prompt and successfully surfaces a prompt injection weakness

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

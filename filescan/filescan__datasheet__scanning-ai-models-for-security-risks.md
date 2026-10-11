<!-- source: https://www.opswat.com/docs/filescan/datasheet/scanning-ai-models-for-security-risks -->

# LLM Scanning

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Artificial intelligence has become part of everyday life. The models behind chatbots, copilots, search engine, and recommendation sit inside the applications people use every day and organizations are adopting open-source and third-party models faster than they can review them.

As models become core software components, scanning them has become a crucial part of cybersecurity. An AI model is not just passive data. In some cases it's an artifact that carries executable code, and an interface that can be manipulated. Most teams pull models from Hugging Face and hope for the best, there isn't much else to go on. However, a model file is a black box, a single model can compromise every system that loads it, or quietly act against the organization that deploys it.

MetaDefender Aether's LLM Scanner checks **the model itself** and **how the model behaves**. That lets teams bring open-source and third-party models into their pipelines, registries, and production systems with confidence.

## [Key features](/docs/filescan/datasheet/scanning-ai-models-for-security-risks#key-features)

- **Multi-format coverage**: supports parsing **7 LLM file types** across the major AI frameworks.
- **Deep structural analysis**: analyzes a model deep down to its structure and **never executes it**.
- **Code & backdoor detection**: exposes embedded payloads, dangerous imports, and hidden execution paths through **30+ dedicated threat indicators**.
- **Built for scale**: supports analyzing **multi-gigabyte models**.
- **Adversarial behavioral probing**: evaluates the live model against a probe suite mapped to **the OWASP LLM Top 10** risk categories.

- **Integrated intelligence**: findings flow into the MetaDefender Aether verdict alongside other analysis layer.
- **MITRE ATLAS mapping:** findings are tagged with technique from MITRE ATLAS, the adversarial-ML knowledge base.

A threat can be baked into the model artifact before it ships, or it can live in how the model responds once deployed. LLM Scanner covers both, through two complementary detection capabilities.

| Feature | Description | Learn more |
| --- | --- | --- |
| **LLM Static Analysis** | Malicious payloads and arbitrary code-execution paths can hide inside model files. The scanner detects the correct format, then parses it down to its structure to surface embedded payloads, dangerous imports, and anomalous signatures. | [Learn more →](/docs/filescan/datasheet/static-analysis) |
| **LLM Dynamic Analysis** | Even a clean model file is no guarantee of safe behavior. The scanner evaluates the deployed model's behaviors itself, dynamically probing it with adversarial prompts to expose prompt injection, sensitive-data disclosure, and other weaknesses that only appear at inference time. | [Learn more →](/docs/filescan/datasheet/dynamic-analysis) |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

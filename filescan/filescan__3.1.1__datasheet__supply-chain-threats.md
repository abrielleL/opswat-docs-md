<!-- source: https://www.opswat.com/docs/filescan/3.1.1/datasheet/supply-chain-threats -->

# Supply Chain Threats

## [#1 Supply Chain Attack](/docs/filescan/3.1.1/datasheet/supply-chain-threats#1-supply-chain-attack)

**Detection Spotlight:** deep staticmalware config

The *SolarWinds* supply chain attack exemplifies how minimal code changes in trusted software can enable massive breaches while bypassing traditional security defenses. Threat actors injected a stealthy backdoor into a legitimate DLL, embedding malicious logic while preserving original functionality. The payload ran silently in a parallel thread mimicking legitimate components. With a valid digital signature and seamless behavior, the DLL evaded detection and granted covert access to thousands of high-profile victims. The compromise of the build pipeline turned trusted updates into a vehicle for global intrusion.

While a 4,000-line backdoor might seem significant, in the context of a large enterprise source code, it’s easily overlooked. This is where MetaDefender Aether excels: it doesn’t just inspect the code, it observes what the software does. It flags deviations from normal behavior, guiding analysts to what really matters—cutting through the noise to spotlight threats that traditional reviews would likely miss.

URL for original DLL

<https://www.filescan.io/uploads/6862920d7423ff017c370754/reports/8fa054eb-8341-4dba-8e64-c1bfc5ce6913/overview>

URL for trojanized DLL

<https://www.filescan.io/uploads/68629132714e106cecb7c676/reports/da0f9ed6-7f46-4cd0-ad98-abaef0c3d8d7/overview>

On the left, we see the legitimate DLL file. On the right is the trojanized version responsible for the infamous SolarWinds incident.

Let’s walk through the key findings as revealed by the sandbox analysis:

String encryption: the code employs a typical obfuscation technique found in various malware: compression followed by base64 encoding.

WMI queries commonly associated with system fingerprinting. In this case, the related strings were encrypted to avoid detection.

Multiple indicators tied to privilege escalation, user identity spoofing, and access control tampering.

---

## [#2 Detect malicious Pickle within AI model](/docs/filescan/3.1.1/datasheet/supply-chain-threats#2-detect-malicious-pickle-within-ai-model)

**Detection Spotlight:** deep static

AI is powering everything from chatbots to business tools. To move faster, companies often use pre-trained AI models shared online through open source platforms like Hugging face. These models are saved in complex formats such as Pickle and PyTorch.

While it is convenience, this usage opens a new risk. Attackers can hide malware inside AI models, especially in Pickle files. Because Pickle can store both data and executable code, it has become a common vehicle for supply chain attacks. A model downloaded from a public repository may look safe but could trigger hidden instructions the moment it is loaded.

A recent case showed how attackers abused the reputation of *Alibaba AI* brand as a lure to publish fake PyPI packages containing a malicious AI model. These packages seem legitimate but contained hidden code to steal user's data and send it to the attacker. Although the packages were available for less than 24 hours on May 19, they were downloaded about 1,600 times. This shows how quickly malicious software can spread through a supply chain attack.

MetaDefender Aether uncovers these threats through dedicated Pickle and PyTorch scanning capabilities.

URL for the sample

<https://www.filescan.io/uploads/68bf95d91b52c70384b7da92/reports/f4cb90b4-279a-47a3-b9ff-69b5e8232bd1/overview>

Multiple Pickle scanning methods from Third-party tools to Deep Static Analysis

REDUCE may be abused for arbitrary code execution and to embed malware in Pickle

Uncovering encoded payload

---

---

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

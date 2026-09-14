<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-sdk-retrieves-real-time-protection-state-of-macos-xprotect -->

# How does SDK retrieves Real-time Protection state of XProtect on macOS?

This article is applied to MetaDefender Endpoint Security SDK releases on **MacOS** with **XProtect**.

## [**Overview**](/docs/mdsdk/knowledge-base/how-sdk-retrieves-real-time-protection-state-of-macos-xprotect#overview)

This article explains how SDK checks and reports the Real-Time Protection (RTP) status of XProtect on macOS. It also describes why we use this approach and the external guidelines that shape our logic.

---

## [**SDK Implementation of GetRealTimeProtectionState** **for XProtect**](/docs/mdsdk/knowledge-base/how-sdk-retrieves-real-time-protection-state-of-macos-xprotect#sdk-implementation-of-getrealtimeprotectionstate-for-xprotect)

Disclaimer

This detection logic is based on publicly available third-party security guidance (recognized by Apple). It may not fully reflect Apple’s internal implementation or any undocumented behavior.

**On macOS Sequoia and later** If `xprotect` CLI tool is available, we use it to query the RTP state directly.

**On Earlier macOS versions** Since the CLI tool is not available, we instead check whether the following XProtect services are loaded:

- `com.apple.XprotectFramework.PluginService`
- `com.apple.XProtect.daemon.scan`

If both services are loaded, we report RTP as **enabled**. If either one is missing, RTP is considered **disabled**.

---

## [**Why we use this logic**](/docs/mdsdk/knowledge-base/how-sdk-retrieves-real-time-protection-state-of-macos-xprotect#why-we-use-this-logic)

Since Apple does not provide:

- Any **official public document** that explains XProtect’s logic or detection methods.
- Any **command or API** that can programmatically enable, disable, or verify XProtect’s RTP state.

When implementing our RTP detection logic, we found no Apple-published specifications that could serve as an authoritative reference.

To make sure our method was **aligned with accepted security practices**, we followed guidance from the [**macOS Security Compliance Project (mSCP)**](https://github.com/usnistgov/macos_security/), which is maintained by the **United States National Institute of Standards and Technology** (NIST).

The **mSCP** provides a programmatic way to generate security guidance for macOS systems. One of its rules, [**os_anti_virus_installed**](https://github.com/usnistgov/macos_security/blob/main/rules/os/os_anti_virus_installed.yaml), requires that:

> *“An approved antivirus product* ***MUST*** *be installed and configured to run.”*

In this context, the antivirus product is **XProtect**.

Finally, Apple itself recognizes the mSCP on their official [**Platform Certifications** page](https://support.apple.com/en-vn/guide/certifications/apc322685bb2/web), which adds credibility to this reference.

---

## [**References**](/docs/mdsdk/knowledge-base/how-sdk-retrieves-real-time-protection-state-of-macos-xprotect#references)

- [GitHub - usnistgov/macos_security: macOS Security Compliance Project](https://github.com/usnistgov/macos_security/)
- [macos_security/rules/os/os_anti_virus_installed.yaml at main · usnistgov/macos_security](https://github.com/usnistgov/macos_security/blob/main/rules/os/os_anti_virus_installed.yaml)
- [macOS Security Compliance Project](https://support.apple.com/en-vn/guide/certifications/apc322685bb2/web)

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

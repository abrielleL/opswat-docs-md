<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/end-of-life-support-for-debian-11-in-metadefender-core -->

# End of Life Support for Debian 11 in MetaDefender Core

View as Markdown Ask ChatGPT about this page Ask Claude about this page

As of August 31, 2026, Debian 11 (Bullseye) will reach its End of Life (EOL), meaning it will no longer receive security updates, patches, or support from the Debian project. In alignment with this timeline, OPSWAT will discontinue MetaDefender Core support for Debian 11 starting **July 1, 2026** — ahead of the official Debian EOL date. This means MetaDefender Core v5.20.0 and later will not support Debian 11. This article outlines the implications, risks, and recommendations for continuing to use this operating system with MetaDefender Core.

## [Background](/docs/mdcore/v5.22.1/knowledge-base/end-of-life-support-for-debian-11-in-metadefender-core#background)

MetaDefender Core relies on the underlying operating system for security updates and stability. With Debian 11 approaching EOL, the Debian project will cease providing updates, leaving systems vulnerable to new security threats. To ensure the security and reliability of MetaDefender Core deployments, OPSWAT strongly recommends upgrading to a supported operating system before July 1, 2026.

## [Impact on MetaDefender Core](/docs/mdcore/v5.22.1/knowledge-base/end-of-life-support-for-debian-11-in-metadefender-core#impact-on-metadefender-core)

Running MetaDefender Core on Debian 11 after its EOL introduces significant risks, including:

- **Security Vulnerabilities:** Without security patches, the operating system is exposed to new exploits and threats.
- **Compatibility Issues:** MetaDefender Core updates and new features may not function correctly on unsupported platforms.
- **Compliance Risks:** Many regulatory standards require systems to run on actively supported operating systems.
- **Lack of Support:** OPSWAT technical support may be limited or unavailable for issues related to EOL operating systems.

## [Recommendations](/docs/mdcore/v5.22.1/knowledge-base/end-of-life-support-for-debian-11-in-metadefender-core#recommendations)

To maintain a secure and supported MetaDefender Core environment, OPSWAT recommends the following:

**Upgrade to a Supported Operating System** Transition to a supported operating system, such as Debian 12 (Bookworm) or Debian 13 (Trixie), which receive active security updates and are fully compatible with the latest MetaDefender Core versions. Refer to the [MetaDefender Core System Requirements](https://www.opswat.com/docs/mdcore/installation/system-requirements) for a complete list of supported platforms.

**Plan Your Migration**

1. **Assess Your Environment:** Identify all systems running Debian 11 with MetaDefender Core installed.
2. **Test Compatibility:** Deploy MetaDefender Core on the new operating system in a staging environment to ensure compatibility with your workflows.
3. **Execute Migration:** Follow OPSWAT's migration guides to transfer configurations, policies, and data to the new platform.
4. **Validate Post-Migration:** Verify that MetaDefender Core operates as expected after the upgrade.

## [Continuing with Debian 11 (Not Recommended)](/docs/mdcore/v5.22.1/knowledge-base/end-of-life-support-for-debian-11-in-metadefender-core#continuing-with-debian-11-not-recommended)

If migration is not immediately feasible, you may choose to remain on MetaDefender Core v5.19.0, the last release to support Debian 11, and pin your engines to specific versions compatible with Debian 11. This approach, however, is not recommended due to the following risks:

- **Security Exposure:** The operating system will remain unpatched after August 31, 2026, increasing the risk of exploitation.
- **Limited Functionality:** You will not receive new features, bug fixes, or performance improvements introduced in later MetaDefender Core versions.
- **Unsupported Configurations:** OPSWAT may not provide support for issues arising from EOL operating systems.
- **Compliance Violations:** Running an EOL operating system may violate organizational or regulatory compliance requirements.

To pin your engine:

1. Access the MetaDefender Core management console.
2. Navigate to **Inventory > Modules**.
3. Select the option to pin the engine to the current version.
4. Save the configuration.

Note:

Staying on v5.19.0 and pinning engine version should only be a temporary measure while planning your migration to a supported operating system.

## [Conclusion](/docs/mdcore/v5.22.1/knowledge-base/end-of-life-support-for-debian-11-in-metadefender-core#conclusion)

The upcoming EOL of Debian 11 poses significant risks to the security and functionality of MetaDefender Core deployments. OPSWAT strongly urges users to upgrade to a supported operating system — such as Debian 12 or Debian 13 — before July 1, 2026, to ensure continued security, compatibility, and support. For assistance with migration or additional guidance, contact [OPSWAT Support](https://www.opswat.com/support) or refer to the [MetaDefender Core Documentation](https://www.opswat.com/docs/mdcore).

Support:

If **Further Assistance** is required, please proceed to log a [****support case or chat with our support engineer****](https://my.opswat.com/portal/support)**.**

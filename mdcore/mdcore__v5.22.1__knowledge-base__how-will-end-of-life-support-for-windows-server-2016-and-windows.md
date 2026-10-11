<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-will-end-of-life-support-for-windows-server-2016-and-windows -->

# How will End of Life Support for Windows Server 2016 and Windows 10 versions before 21H2 in MetaDefender Core affect my deployments?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdcore/v5.22.1/knowledge-base/how-will-end-of-life-support-for-windows-server-2016-and-windows#overview)

Microsoft has announced the end-of-life (EOL) for [Windows Server 2016](https://learn.microsoft.com/en-us/lifecycle/products/windows-server-2016) and [Windows 10 versions prior to 21H2](https://learn.microsoft.com/en-us/windows/release-health/release-information), marking the end of official support and security updates for these platforms. As a result, OPSWAT will no longer support MetaDefender Core installations on these operating systems starting October 2025. To maintain platform compatibility, security, and compliance, organizations should begin planning a transition to a supported operating system well ahead of this date.

This article outlines the impact of these EOL dates on OPSWAT MetaDefender Core deployments, including supported operating systems, recommended actions, and upgrade paths to ensure continued security and compliance.

## [Affected Operating Systems](/docs/mdcore/v5.22.1/knowledge-base/how-will-end-of-life-support-for-windows-server-2016-and-windows#affected-operating-systems)

- **Windows Server 2016**: Mainstream support ended on January 11, 2022, with extended support ending on **January 12, 2027**. After this date, Microsoft will no longer provide security updates, non-security updates, or technical support for Windows Server 2016.
- **Windows 10 Versions Prior to 21H2**: All Windows 10 versions before 21H2 (e.g., 20H2, 2004, 1909, etc.) have reached or will soon reach their EOL. For example:

  - Windows 10 20H2 reached EOL on **May 10, 2022** (Enterprise and Education editions on **May 9, 2023**).
  - Windows 10 21H1 reached EOL on **December 13, 2022**.
  - Other earlier versions (e.g., 1909, 2004) are already out of support.

After these EOL dates, Microsoft will no longer provide security patches or updates, increasing the risk of vulnerabilities and compatibility issues with MetaDefender Core.

## [Impact on MetaDefender Core](/docs/mdcore/v5.22.1/knowledge-base/how-will-end-of-life-support-for-windows-server-2016-and-windows#impact-on-metadefender-core)

MetaDefender Core relies on the underlying operating system for stability, security, and compatibility with its advanced threat **protection features including MetaScan Multiscanning, Deep CDR, Proactive DLP, Adaptive Sandbox, and File-based Vulnerability Assessment.** Running MetaDefender Core on unsupported operating systems like Windows Server 2016 or Windows 10 versions prior to 21H2 may result in:

- **Security Risks**: Lack of security patches from Microsoft increases exposure to malware, zero-day attacks, and other cyber threats.
- **Compatibility Issues**: MetaDefender Core updates and new features may not function correctly on unsupported operating systems, leading to degraded performance or unexpected behavior.
- **Compliance Violations**: Failure to update operating systems can lead to regulatory and compliance violations (e.g., PCI-DSS, HIPAA).

## [Supported Operating Systems](/docs/mdcore/v5.22.1/knowledge-base/how-will-end-of-life-support-for-windows-server-2016-and-windows#supported-operating-systems)

To ensure optimal performance and security, OPSWAT recommends deploying MetaDefender Core on the following supported Windows operating systems:

- **Windows Server**: Windows Server 2019, Windows Server 2022, Windows Server 2025
- **Minimum System Requirements**:

  - CPU: 8 vCPUs
  - RAM: 8 GB (16 GB or more recommended)
  - Disk Space: 50 GB free disk space for installation and operation
  - .NET Framework: Version 4.8 or later

For the latest supported operating systems and system requirements, refer to the [MetaDefender Core Documentation](/docs/mdcore/v5.22.1/installation/metadefender-core-documentation).

## [Recommended Actions](/docs/mdcore/v5.22.1/knowledge-base/how-will-end-of-life-support-for-windows-server-2016-and-windows#recommended-actions)

To maintain a secure and compliant MetaDefender Core deployment, OPSWAT strongly advises the following steps:

1. **Upgrade Operating Systems**:

   - For Windows Server 2016, migrate to **Windows Server 2019** or **Windows Server 2022** **or 2025**. Microsoft provides upgrade paths via in-place upgrades or clean installations. Refer to Microsoft’s Windows Server Upgrade Documentation for guidance.
   - For Windows 10 versions prior to 21H2, upgrade to **Windows 10 22H2** or **Windows 11** to receive ongoing security updates and support. Use the Windows Update feature or download the latest ISO from Microsoft’s Download Center.
2. **Plan Ahead for EOL**:

   - Develop a migration plan well in advance of the EOL dates to avoid disruptions. Test MetaDefender Core on the target operating system in a staging environment before production deployment.
   - Update any scripts, automation, or integrations that rely on the current operating system to ensure compatibility with the new OS.
3. **Leverage MetaDefender Cloud Image Deployment Options**:

   - For AWS users, consider deploying MetaDefender Core using the latest AMIs (Amazon Machine Images) available on the AWS Marketplace, which support Windows Server 2019 and 2022. Refer to the [How to deploy using AWS services](/docs/mdcore/v5.22.1/cloud-deployment/aws-deployments).
   - Use CloudFormation scripts for streamlined deployment, which can reduce setup time to approximately 3–12 minutes depending on the deployment model (single or distributed).
4. **Contact OPSWAT Support**:

   - If you need assistance with upgrading or migrating MetaDefender Core, contact the OPSWAT support team by [**creating a support case or chatting with our support engineer**](https://my.opswat.com/support).
   - For licensing inquiries or custom deployment options, reach out to [sales-inquiry@opswat.com](mailto:sales-inquiry@opswat.com).

## [Upgrade Process](/docs/mdcore/v5.22.1/knowledge-base/how-will-end-of-life-support-for-windows-server-2016-and-windows#upgrade-process)

1. **Backup Configuration**: Before upgrading the operating system, back up your MetaDefender Core configuration, including scan engine settings, policies, and logs. Refer to the MetaDefender Core Operating Guide for backup instructions.
2. **Test Compatibility**: Install MetaDefender Core on a test instance running the target operating system (e.g., Windows Server 2022 or Windows 11) to verify compatibility with your workflows and integrations.
3. **Perform Upgrade**:

   - For Windows Server, follow Microsoft’s in-place upgrade process or deploy a new instance with the updated OS and reinstall MetaDefender Core.
   - For Windows 10, use the Windows Update Assistant or a clean installation to upgrade to 22H2 or Windows 11.
4. **Validate Deployment**: After upgrading, verify that MetaDefender Core functions correctly, including file scanning, Deep CDR, and integration with services like Amazon S3 or SQS (if applicable).
5. **Monitor and Update**: Regularly check for MetaDefender Core updates and apply them to ensure compatibility with the latest security features and threat intelligence.

## [Additional Resources](/docs/mdcore/v5.22.1/knowledge-base/how-will-end-of-life-support-for-windows-server-2016-and-windows#additional-resources)

- [Microsoft Windows Server 2016 Lifecycle](https://learn.microsoft.com/en-us/lifecycle/products/windows-server-2016)
- [Microsoft Windows 10 Release Information](https://learn.microsoft.com/en-us/windows/release-health/release-information)
- [MetaDefender Core Release Notes](https://www.opswat.com/docs/mdcore/release-notes)
- [OPSWAT MetaDefender Core Documentation](https://www.opswat.com/docs/mdcore)

## [Conclusion](/docs/mdcore/v5.22.1/knowledge-base/how-will-end-of-life-support-for-windows-server-2016-and-windows#conclusion)

The end-of-life for Windows Server 2016 and Windows 10 versions prior to 21H2 requires proactive planning to maintain a secure and compliant MetaDefender Core deployment. By upgrading to supported operating systems like Windows Server 2019/2022, organizations can ensure continued protection against malware, zero-day attacks, and data breaches. For further assistance, contact OPSWAT’s support or sales teams to explore deployment options and licensing tailored to your needs.

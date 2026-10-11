<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/end-of-life-support-for-centos-7-and-RedHat-7-in-metadefender-co -->

# End-of-Life Support for CentOS 7 and RedHat 7 in MetaDefender Core and Engines

View as Markdown Ask ChatGPT about this page Ask Claude about this page

In line with industry standards and our commitment to providing secure and efficient solutions, OPSWAT will discontinue support for CentOS 7 and RedHat 7 in MetaDefender Core and its associated engines. This article details the implications of this change, outlines the operating systems that will be supported moving forward, and provides essential guidance for users who may need to continue using CentOS 7 or RedHat 7 temporarily.

CentOS 7 and RedHat 7 has been a reliable platform for many users, but it has now reached its end-of-life phase. Supporting an outdated operating system increases security risks and prevents access to new features and improvements. Therefore, MetaDefender Core and its engines will no longer support CentOS 7 and RedHat 7 after December 2024.

## [Supported Operating Systems Moving Forward](/docs/mdcore/v5.22.1/knowledge-base/end-of-life-support-for-centos-7-and-RedHat-7-in-metadefender-co#supported-operating-systems-moving-forward)

To ensure optimal performance and security, we encourage all users to transition from CentOS 7 or RedHat 7 to the following supported operating systems for MetaDefender Core and its engines:

- Red Hat Enterprise Linux (RHEL) 8, 9
- Debian 11
- Ubuntu 20.04, 22.04
- Amazon Linux 2 is supported via Amazon Machine Image (AMI)

Important Notice

If you do not transition to a supported operating system, you will no longer receive the latest updates and features from OPSWAT MetaDefender Core and its engines. This could significantly impact the functionality and security of your system.

## [Continuing with CentOS 7/RedHat 7 - Pinning Your Engine [ Not Recommended]](/docs/mdcore/v5.22.1/knowledge-base/end-of-life-support-for-centos-7-and-RedHat-7-in-metadefender-co#continuing-with-centos-7redhat-7---pinning-your-engine--not-recommended)

We understand that some users may need additional time to transition from CentOS 7/RedHat 7. If you choose to continue using these engines temporarily, it is crucial to take the following steps **before December 2024**:

- **Pin Your Engine Version**: MetaDefender Core engines are configured by default to receive automatic updates. While this ensures systems stay up-to-date with the latest features, it can cause issues on unsupported operating systems like CentOS 7 after it reaches End-of-Life. By pinning your engine version, you can prevent automatic updates that may not be compatible with these operating systems, thus maintaining system stability during your transition period.

  - How to Pin the Engine:

    - Access your MetaDefender Core configuration settings.
    - Go to the Inventory section and click on the Modules.
    - For each available engine, click on it and pin the current version and database to prevent automatic updates.

- **Plan Your Migration**: Begin planning your transition to a supported operating system as soon as possible. Delaying this process can expose your system to security vulnerabilities and compliance risks.

## [Conclusion](/docs/mdcore/v5.22.1/knowledge-base/end-of-life-support-for-centos-7-and-RedHat-7-in-metadefender-co#conclusion)

The End-of-Life support for CentOS 7 and RedHat 7 in MetaDefender Core and its engines is a necessary step towards providing a more secure and efficient experience for our users. We strongly recommend upgrading to one of the supported operating systems listed above to continue receiving updates and support. If you must remain on CentOS 7 or RedHat 7 temporarily, ensure you pin your engine version before December 2024 and expedite your migration plan to a supported platform.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).

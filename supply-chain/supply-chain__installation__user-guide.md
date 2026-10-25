<!-- source: https://www.opswat.com/docs/supply-chain/installation/user-guide -->

# User Guide

### About this guide

Welcome to the MetaDefender Software Supply Chain guide. This guideline is intended to provide the information you need to:

- Install, set up, and configure the product to begin scanning source code and docker images from various repositories (GitHub, DockerHub, Amazon ECR, Quay, etc.)
- Seamlessly integrate with your preferred version control and container registry provider(s)
- Initiate the analysis process to scan for malware, secrets or open source vulnerabilities
- Get actionable intelligence via a real-time comprehensive dashboard or emailed automated reports
- Learn about new features, updated features, and bug fixes
- Learn about frequently asked questions and additional concepts through our library of knowledge base article

### Service integrations

| **Service Category** | **Service Vendor** |
| ---- | ---- |
| Source Code Services | GitHub & GitHub Enterprise |
|  | Bitbucket Cloud & Bitbucket Data Center |
|  | GitLab |
|  | Gitea |
|  | SVN |
|  | Azure DevOps |
| Container Services | DockerHub |
|  | JFrog Containers |
|  | Amazon Elastic Container Registry (ECR) |
|  | Quay |
|  | Azure Container Registry (ACR) |
|  | Harbor |
|  | Sonatype Nexus Repository (Nexus Container) |
| Binary Services | JFrog Artifactory |
|  | Sonatype Nexus Repository (Nexus Binary) |

**MetaDefender Software Supply Chain** offers enterprises the ability to protect their stored data from malicious malware attacks, data breaches and Zero-Day threats by using OPSWAT’s industry-leading Multiscanning and SBOM detection technologies. It helps organizations avoid compliance violations such as leaking sensitive data by leveraging the secret detection module.

The ability to view all the data stored in multiple cloud-based storage and collaboration solutions like GitHub repositories, container services such as DockerHub, Amazon ECR, and Quay and binary services like JFrog Artifactory provides IT professionals insight into the health of their entire storage at any given time. This comprehensive coverage ensures visibility into the status and performance of both source code repositories and containerized applications across various cloud-based platforms.

Automated and actionable reports identify threats and risks associated with users and services for quick remediation actions.

With the native integration between MetaDefender Software Supply Chain and MetaDefender Core, immediate detection, remediation, and prevention of malicious content is ensured.

> **Info**
>
> Learn more about the Software Bill of Materials (SBOM) technology and the importance of staying compliant and secure in the software supply chain by visiting [opswat.com/technologies/sbom](https://www.opswat.com/technologies/sbom).

**MetaDefender Software Supply Chain** **offers the following capabilities:**

- Integration with:
  - Source code services such as GitHub, GitLab, Svn, Gitea, Bitbucket Cloud and DataCenter
  - Container services such as DockerHub, Amazon ECR, Quay, JFrog Containers, Azure Containers, Harbor Registry Containers and Sonatype Nexus Repository
  - Binary services such as JFrog Artifactory and Sonatype Nexus Repository
- Unified Dashboard
- Superior Reporting
- Report History
- Easy Setup and Integrations
- User Management
- Automation and Customization of Workflows
- [Event based scanning](https://www.opswat.com/docs/supply-chain/operating/triggering-an-automatic-scan): a push, a pull request or a new artifact starts a scan automatically
- [Cross Domain Transfer](https://www.opswat.com/docs/supply-chain/configuration/cross-domain-transfer): scanned code and images move from a Low Side to a High Side environment
- Monitoring and Logging for all user actions
- Technologies:
  - Malware scanning with 5 AVs (default package): ClamAV, Avira, AhnLab, Varist, Tachyon.
  - Proactive DLP detects secrets in your source code and container.
  - SBOM detects opensource vulnerabilities, licenses.
  - [Cryptography](https://www.opswat.com/docs/supply-chain/operating/cryptography) (CBOM) finds the cryptographic assets in scanned content and shows if they are quantum safe.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)

<!-- source: https://www.opswat.com/docs/mdcore/cloud-deployment/azure-deployments -->

# Deploy using Azure services

### [Introduction](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#introduction)

This Deployment Guide provides step-by-step instructions for deploying MetaDefender Core on Azure Cloud Services infrastructure.

Organizations interested in protecting their solutions deployed in Azure can leverage MetaDefender to analyze and sanitize files residing, or transitioning, their Azure deployment. MetaDefender can scan and either sanitize or check for known vulnerabilities, depending on the type of traffic it's seeing. The ideal use case would be an organization that allows files to be uploaded to Azure through an external facing web portal. Analyzing files before they are made accessible to the end-users is critical to ensure that no malicious content is allowed and distributed through the web application.

Advanced attacks are concealing the malicious payload and are relying on productivity files (documents, pdfs, images) as a distribution mechanism. Productivity files allow active content to be leveraged, but these features are frequently exploited to execute the malicious behavior.

This guide is for IT infrastructure architects, administrators and DevOps professionals who are seeking to prevent potential malicious traffic being allowed in their Axure Cloud deployment. Threat Prevention is ensured for both productivity files that might be uploaded and for known vulnerabilities that can be identified for all running services/applications deployed in Azure. The vulnerability scanning is checking known vulnerabilities for unpatched OS and running applications.

MetaDefender is provided as:

- AMI through the Azure Marketplace ([MetaDefender products](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=MetaDefender&page=1))
- Packaged installer available for download through the [OPSWAT Portal](https://portal.opswat.com/).
- Container Image available in the [OPSWAT Docker Hub Repository](https://hub.docker.com/u/opswat)

There are currently no restrictions on Azure regions in which you can deploy MetaDefender. The only restriction is that MetaDefender is not available Azure for Government at this time.

**OPSWAT Contact Information**

**Sales:**[sales-inquiry@opswat.com](mailto:sales-inquiry@opswat.com)

**Support:**<https://www.opswat.com/support>

**Other:**<https://www.opswat.com/contact>

For deploying our solution in Azure, please review the guideline listed below:

- [AKS Cluster](/docs/mdcore/cloud-deployment/aks-cluster-provision)

### [Database Encryption](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#database-encryption)

MetaDefender Core supports both native OS encryption or Azure disk encrypted volumes. The database is secured via credentials and can be configured to encrypt everything at rest. In general, OPSWAT recommends the use of a 3rd party database layer, e.g. Azure PostgreSQL, which should be encrypted. It is best practice to not share the database layer on the same hosts/Azure VM

### [Sensitive Data Storage](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#sensitive-data-storage)

Network traffic processed by MetaDefender Core is SSL encrypted during transmission. The product does not collect or store any customer data outside of analyzing the contents of files submitted for scanning.

During the scanning process, files are stored unencrypted on disk to allow the scan process to complete. Once the scan completes, the file is deleted unless configured to place the file in quarantine. If you wish to encrypt these quarantined files, please use native OS encryption or Azure Disk encrypted volumes.

### [Private Key Management](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#ec2-key-management)

The Private key pair is only used to SSH or RDP to the Azure VM. This is a very uncommon scenario, used primarily for debugging. You can create a new key pair, or use an existing pair.

### [Costs](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#costs)

MetaDefender is made available as an annual subscription. The only mandatory service that needs to be purchase is MetaDefender Core. MetaDefender Core is a paid service and is currently licensed on the BYOL (Bring Your Own License) model. Contact our sales team via our Contact form, available here: <https://www.opswat.com/contact>

Considering that are over 60 different options to license MetaDefender, it is highly coupled to the use case and the advanced features that you are considering deploying. Note that the more functionality you are adding to MetaDefender, the more need will be of CPU from the EC2 instance.

Our recommendation would be a minimum 8 vCPU for our lower tiers.

We recommend to go with Reserved Instances, considering that you are committing to an annual subscription for MetaDefender.

For pricing per vm, please refer to the official [Azure pricelist](https://azure.microsoft.com/en-us/pricing/details/virtual-machines/linux/)

### [Sizing](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#sizing)

MetaDefender needs an Azure vm with minimum 8 vCPU, in order to have an optimal response rate to submitted files for analysis. However, depending on the use case and expected throughput (analysis SLA), higher tier instances are recommended.

The system requirements (hardware and supported operating system) are defined here: [Recommended System Configuration](/docs/mdcore/installation/recommended-system-configuration)

## [Operation Guidance for Azure VM deployments](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#operation-guidance-for-ec2-deployments)

### [Troubleshooting](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#troubleshooting)

For troubleshooting MetaDefender Core with Azure deployment , please refer to the following guides:

1. [Troubleshooting MetaDefender Core](/docs/mdcore/troubleshooting/troubleshooting-metadefender-core) (installation, logging, node management)
2. [Scripted license management](/docs/mdcore/installation/scripted-license-management) (Licensing status and automation)
3. [Performance Scaling](/docs/mdcore/knowledge-base/how-can-i-increase-parallel-count-and-max-queue-size) (for large deployments)
4. Engine and Database health (view Health Check section under different deployment option)

### [Routine Maintenance](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#routine-maintenance)

Always update the MetaDefender deployment with the new versions published either on:

- [portal.opswat.com](http://portal.opswat.com/) > Products section
- Azure Marketplace

Release Notes are available [here](/docs/mdcore/release-notes/release-notes).

MetaDefender provides a direct update mechanism for the licensed analysis engines (all the engines listed in Inventory > Technology). The application logic will require a product update, however the licensed engines are automatically updated (in online deployments). Both the engine and the signature updates for Anti-malware engines will be automatically downloaded and deployed on a daily basis. We recommend to configure the product to check for updates at least every 4h (for more details see [Engines Update Configuration](/docs/mdcore/configuration/engines-update-configuration)).

In general MetaDefender instance has Internet connection. If an offline deployment is considered, make sure you are using either the Central Management or the Update Downloader and that you are uploading the engines' signatures updates minimum once a day.

If you are deploying MetaDefender in your own AWS environment, the AWS service limits will not impact the product. A potential issue that can be caused by AWS service is using a lower-tier EC2 type than is recommended. Please see the Costs section above for details on which EC2 instance types we recommend for MetaDefender. Network bandwidth and EBS/General SSD IOPS can become a limitation in high-throughput environments. The solution to this is to simply use higher tier machines such as ones with 20+Gbps network bandwidth and moving to a provisioned IOPS (io2) disk(s).

MetaDefender supports the ability to rotate system credential and cryptographic keys to ensure the security of your deployment. Information for performing this rotation can be found on the [Database Management](/docs/mdcore/configuration/database-management) page. MetaDefender users can also change user credentials via our [POST - Change Password](https://docs.opswat.com/metadefender-core/ref#userchangepass) API.

### [Emergency Maintenance](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#emergency-maintenance)

In case of any availability failures of an AWS Service, recommended actions would be to pass the load to another MetaDefender instances, preferably deployed in a different AZ than the one affected. Any analysis in progress submitted to MetaDefender will be considered lost. However, is highly recommended to build a resilient system that won't rely on MetaDefender to recover the pending jobs, but to be managed by a queueing mechanism. See Backup and Recovery suggested deployment scenarios.

## [Support](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#support)

To receive support, please visit our Support Portal. From there after you log in click on "Cases" on menu at the top of the page and then click "New" on the right hand side to create a new case.

Support policies, costs, levels and SLA's are described on our website, at the Support section: <https://www.opswat.com/support>. Please view our support tiers in the table below:

*Note: Please visit*<https://www.opswat.com/support>*for the most updated information on support.*

|  | **Standard** | **Gold** | **Platinum** |
| --- | --- | --- | --- |
| **Prices** | Included with your license | 20%  ($500.00 minimum) * | 25%  ($2000.00 minimum) * |
| *_Support Hours  *_ |  |  |  |
| Support via Portal Ticket System | 8AM to 5PM  business days  (local to you) | 7AM to 7PM  business days  (local to you) | 24 x 7 x 365 |
| Support via Chat | 8AM to 5PM  business days  (local to you) | 7AM to 7PM  business days  (local to you) | 24 x 7 x 365 |
| Support via Phone |  |  | 24 x 7 x 365 |
| **Incident Response Times** |  |  |  |
| Blocker Issues First Response Times | Within 1 business day | Within 2 hours | Within 1 hour |
| Non-blocker Issues First Response Times | Within 3 business days | Within 2 business days | Within 1 business day |
| **Support Account Management** |  |  | Yes |
| Support Account Manager |  |  | Yes |
| Quarterly Conference Call Reviews |  |  | Yes |
| Yearly Roadmap Review with the Product Team |  |  | Yes |
| Quarterly Summary Reports |  | Yes | Yes |

Info

The following sections are for Azure deployments. When installing MetaDefender Core in Kubernetes check [Installing MetaDefender Core in K8S](/docs/mdcore/container-deployment/metadefender-core-in-your-already-created-k8s)

## [Reference Materials](/docs/mdcore/cloud-deployment/azure-deployments#reference-materials)

All MetaDefender documentation is available on [docs.opswat.com/mdcore](https://docs.opswat.com/metadefender-core/v4.21.1/)

## [Localization](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#localization)

MetaDefender products and documentation are available exclusively in English for now.

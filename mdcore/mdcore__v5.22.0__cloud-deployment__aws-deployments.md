<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments -->

# How to deploy using AWS services

### [Introduction](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#introduction)

This Deployment Guide provides step-by-step instructions for deploying MetaDefender Core on Amazon Web Services infrastructure.

Organizations interested in protecting their solutions deployed in AWS can leverage MetaDefender to analyze and sanitize files residing, or transitioning, their AWS deployment. MetaDefender can scan and either sanitize or check for known vulnerabilities, depending on the type of traffic it's seeing. The ideal use case would be an organization that allows files to be uploaded to AWS through an external facing web portal. Analyzing files before they are made accessible to the end-users is critical to ensure that no malicious content is allowed and distributed through the web application.

Advanced attacks are concealing the malicious payload and are relying on productivity files (documents, pdfs, images) as a distribution mechanism. Productivity files allow active content to be leveraged, but these features are frequently exploited to execute the malicious behavior.

This guide is for IT infrastructure architects, administrators and DevOps professionals who are seeking to prevent potential malicious traffic being allowed in their AWS Cloud deployment. Threat Prevention is ensured for both productivity files that might be uploaded and for known vulnerabilities that can be identified for all running services/applications deployed in AWS. The vulnerability scanning is checking known vulnerabilities for unpatched OS and running applications.

MetaDefender is provided as:

- AMI through the AWS Marketplace ([MetaDefender products](https://aws.amazon.com/marketplace/seller-profile?id=1d722262-54b5-4258-b5fc-d01324b7a416))
- Packaged installer available for download through the [My OPSWAT](https://my.opswat.com)
- Helm Charts for MetaDefender products in [GitHub](https://github.com/OPSWAT/metadefender-k8s) together with the container images available in the [OPSWAT Docker Hub Repository](https://hub.docker.com/u/opswat)

There are currently no restrictions on AWS regions in which you can deploy MetaDefender. The only caveat is that MetaDefender is not available in AWS GovCloud at this time.

**OPSWAT Contact Information**

**Sales:**[sales-inquiry@opswat.com](mailto:sales-inquiry@opswat.com)

**Support:**<https://www.opswat.com/support>

**Other:**<https://www.opswat.com/contact>

For installing our solution, please review the guideline listed below:

- [Single EC2](/docs/mdcore/v5.22.0/cloud-deployment/single-ec2-deployment)
- [Autoscaling EC2](/docs/mdcore/v5.22.0/cloud-deployment/autoscaling-ec2-deployment)
- [EKS Cluster](/docs/mdcore/v5.22.0/cloud-deployment/eks-cluster-provision)

### [Database Configuration](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#database-configuration)

MetaDefender Core supports Amazon Aurora or AWS RDS that are service that deploy PostgreSQL servers provided by AWS. This section information is extended in [AWS Database Services](/docs/mdcore/v5.22.0/cloud-deployment/aws-database-services)

### [EC2 Key Management](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#ec2-key-management)

The EC2 key pair is only used to SSH or RDP to the EC2 instance. This is a very uncommon scenario, used primarily for debugging. You can create a new key pair, or use an existing pair.

### [Costs](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#costs)

MetaDefender is made available as an annual subscription. The only mandatory service that needs to be purchase is MetaDefender Core. MetaDefender Core is a paid service and is currently licensed on the BYOL (Bring Your Own License) model. Contact our sales team via our Contact form, available here: <https://www.opswat.com/contact>

Considering that are over 60 different options to license MetaDefender, it is highly coupled to the use case and the advanced features that you are considering deploying. Note that the more functionality you are adding to MetaDefender, the more need will be of CPU from the EC2 instance.

Our recommendation would be a minimum 8 vCPU for our lower tiers.

We recommend General Purpose (m family) and Compute Optimized (c family) instance types, preferably that are using NVMe-based SSDs for high throughput expectations:

- m5.xlarge
- m5.2xlarge
- m5.4xlarge
- c5d.2xlarge
- c5d.4xlarge
- c5d.8xlarge

We recommend to go with Reserved Instances, considering that you are committing to an annual subscription for MetaDefender.

For pricing per instance, please refer to the official AWS pricelist: <https://aws.amazon.com/ec2/pricing/>

### [Sizing](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#sizing)

MetaDefender needs an EC2 instance with minimum 8 vCPU, in order to have an optimal response rate to submitted files for analysis. However, depending on the use case and expected throughput (analysis SLA), higher tier instances are recommended.

The system requirements (hardware and supported operating system) are defined here: [Recommended System Configuration](/docs/mdcore/v5.22.0/installation/recommended-system-configuration)

## [Operation Guidance for EC2 deployments](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#operation-guidance-for-ec2-deployments)

### [Monitoring](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#monitoring)

For monitoring indications please read the [Monitoring in AWS](/docs/mdcore/v5.22.0/cloud-deployment/monitoring-in-aws) page created for this topic.

### [Troubleshooting](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#troubleshooting)

For troubleshooting indications please read the [troubleshooting page](/docs/mdcore/v5.22.0/cloud-deployment/troubleshooting) created for this topic.

### [Backup and Recovery](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#backup-and-recovery)

MetaDefender service in general does not store any persistent data that needs to be recovered or backed-up. Regardless if it's a hardware or service failure, MetaDefender will not recover the files submitted in the queue and those files will need to be resubmitted for analysis. Using OPSWAT Central Management (OCM) or a central database (such as AWS Aurora/RDS), there is no backup required per service. All configurations will automatically be shared with the new instances when they are brought up (this is the recommended model to prevent data loss). In order to have a sustainable service, not affected by any hardware or software failures, the recommendations are to:

- Store the files in an S3 bucket before they are submitted to MetaDefender

  - In order to avoid any AZ or Region failure, would be recommended to use S3's Cross-Region Replication
- Define a pool of jobs for your webapp, which are in a pending state while MetaDefender analyzes the files

  - Best option would be to use the SQS service and your application to send the files from the SQS to MetaDefender

    - Every time the files are being uploaded to a temporary S3 bucket, there is a new job added to the SQS
  - If MetaDefender fails, the job is stilled defined in SQS
  - If AZ or even the region fails, if the S3 bucket is synced in multiple regions, the SQS queue should be easily be able to be reconstructed for the remaining files in the bucket

    - On initializing stage, check the files in the S3 bucket and if there is any file left, add them to the SQS
- Based on the result from MetaDefender, the file should be moved to the final location or it's sanitized copy should. Either way, the original file should be deleted from the temporary S3 bucket
- When the job is being removed from SQS, remove also the file from the S3 bucket

In case of failure of MetaDefender service, follow the instructions defined in the Troubleshooting section: [Troubleshooting MetaDefender Core](/docs/mdcore/v5.22.0/troubleshooting/troubleshooting-metadefender-core)

## [Support](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#support)

To receive support, please visit our Support Portal. From there after you log in click on "Cases" on menu at the top of the page and then click "New" on the right hand side to create a new case.

Support policies, costs, levels and SLA's are described on our website, at the Support section: <https://www.opswat.com/support>. Please view our support tiers in the table below:

*Note: Please visit*<https://www.opswat.com/support>*for the most updated information on support.*

|  | **Standard** | **Gold** | **Platinum** |
| --- | --- | --- | --- |
| **Prices** | Included with your license | 20%  ($500.00 minimum) * | 25%  ($2000.00 minimum) * |
| **Support Hours** |  |  |  |
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

## [Accessibility](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#accessibility)

## [Reference Materials](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#reference-materials)

All MetaDefender documentation is available on [docs.opswat.com/mdcore](/docs/mdcore)

## [Localization](/docs/mdcore/v5.22.0/cloud-deployment/aws-deployments#localization)

MetaDefender products and documentation are available exclusively in English for now.

<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/cloud-deployment/troubleshooting -->

# Troubleshooting and Maintenance

View as Markdown Ask ChatGPT about this page Ask Claude about this page

For troubleshooting MetaDefender Core with Kubernetes deployment , please refer to the following guides:

1. [Troubleshooting K8S](/docs/mdcore/v5.22.1/container-deployment/troubleshooting)(installation, logging, cluster management tools)

For troubleshooting MetaDefender Core with EC2 deployment , please refer to the following guides:

1. [Troubleshooting MetaDefender Core](/docs/mdcore/v5.22.1/troubleshooting/troubleshooting-metadefender-core) (installation, logging, node management)
2. [Scripted license management](/docs/mdcore/v5.22.1/installation/scripted-license-management) (Licensing status and automation)
3. [Performance Scaling](/docs/mdcore/v5.22.1/knowledge-base/how-can-i-increase-parallel-count-and-max-queue-size) (for large deployments)
4. [AWS Database Troubleshooting](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Troubleshooting.html) (AWS Docs for RDS)

### [Regular Instance Maintenance](/docs/mdcore/v5.22.1/cloud-deployment/troubleshooting#regular-instance-maintenance)

Please see this page for more information on [Regular Maintenance](/docs/mdcore/v5.22.1/operating/regular-maintenance) of the MetaDefender Core services and components. For database maintenance, please refer to [Database Defragmentation and Optimization](/docs/mdcore/v5.22.1/operating/database-defragmentation-and-optimization).

### [Routine Maintenance](/docs/mdcore/v5.22.1/cloud-deployment/troubleshooting#routine-maintenance)

Always update the MetaDefender deployment with the new versions published either on:

- [portal.opswat.com](http://portal.opswat.com/) > Products section
- AWS Marketplace

Release Notes are available [here](/docs/mdcore/v5.22.1/release-notes/release-notes).

MetaDefender provides a direct update mechanism for the licensed analysis engines (all the engines listed in Inventory > Technology). The application logic will require a product update, however the licensed engines are automatically updated (in online deployments). Both the engine and the signature updates for Anti-malware engines will be automatically downloaded and deployed on a daily basis. We recommend to configure the product to check for updates at least every 4h (for more details see [Engines Update Configuration](/docs/mdcore/v5.22.1/configuration/engines-update-configuration)).

In general MetaDefender instance has Internet connection. If an offline deployment is considered, make sure you are using either the Central Management or the Update Downloader and that you are uploading the engines' signatures updates minimum once a day.

If you are deploying MetaDefender in your own AWS environment, the AWS service limits will not impact the product. A potential issue that can be caused by AWS service is using a lower-tier EC2 type than is recommended. Please see the Costs section above for details on which EC2 instance types we recommend for MetaDefender. Network bandwidth and EBS/General SSD IOPS can become a limitation in high-throughput environments. The solution to this is to simply use higher tier machines such as ones with 20+Gbps network bandwidth and moving to a provisioned IOPS (io2) disk(s).

MetaDefender supports the ability to rotate system credential and cryptographic keys to ensure the security of your deployment. Information for performing this rotation can be found on the [Database Management](/docs/mdcore/v5.22.1/configuration/database-management) page. MetaDefender users can also change user credentials via our [POST - Change Password](/docs/mdcore/v5.22.1/metadefender-core#userchangepass) API.

### [Emergency Maintenance](/docs/mdcore/v5.22.1/cloud-deployment/troubleshooting#emergency-maintenance)

In case of any availability failures of an AWS Service, recommended actions would be to pass the load to another MetaDefender instances, preferably deployed in a different AZ than the one affected. Any analysis in progress submitted to MetaDefender will be considered lost. However, is highly recommended to build a resilient system that won't rely on MetaDefender to recover the pending jobs, but to be managed by a queueing mechanism (e.g. [AWS SQS](https://aws.amazon.com/sqs/)). See Backup and Recovery suggested deployment scenarios.

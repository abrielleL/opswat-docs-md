<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/installation/troubleshooting-and-maintenance -->

# Troubleshooting and Maintenance

View as Markdown Ask ChatGPT about this page Ask Claude about this page

For troubleshooting MetaDefender ICAP with Kubernetes deployment , please refer to the following guides:

1. [Troubleshooting Containers](/docs/mdicap/v5.15.0/installation/troubleshooting-containers) (installation, logging, cluster management tools)

For troubleshooting MetaDefender ICAP with EC2 deployment , please refer to the following guides:

1. [How to read the MetaDefender ICAP Server log](/docs/mdicap/v5.15.0/troubleshooting/how-to-read-the-metadefender-icap-server-log) to read(installation, logging, node management)
2. [AWS Database Troubleshooting](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Troubleshooting.html) (AWS Docs for RDS)

### [Routine Maintenance](/docs/mdicap/v5.15.0/installation/troubleshooting-and-maintenance#routine-maintenance)

Always update the MetaDefender deployment with the new versions published either on:

- [portal.opswat.com](http://portal.opswat.com/) > Products section
- AWS Marketplace

Release Notes are available [here](/docs/mdicap/v5.15.0/release-notes/release-notes).

If you are deploying MetaDefender in your own AWS environment, the AWS service limits will not impact the product. A potential issue that can be caused by AWS service is using a lower-tier EC2 type than is recommended. Please see the Costs section above for details on which EC2 instance types we recommend for MetaDefender. Network bandwidth and EBS/General SSD IOPS can become a limitation in high-throughput environments. The solution to this is to simply use higher tier machines such as ones with 20+Gbps network bandwidth and moving to a provisioned IOPS (io2) disk(s).

### [Emergency Maintenance](/docs/mdicap/v5.15.0/installation/troubleshooting-and-maintenance#emergency-maintenance)

In case of any availability failures of an AWS Service, recommended actions would be to pass the load to another MetaDefender instances, preferably deployed in a different AZ than the one affected. Any analysis in progress submitted to MetaDefender will be considered lost. However, is highly recommended to build a resilient system that won't rely on MetaDefender to recover the pending jobs, but to be managed by a queueing mechanism (e.g. [AWS SQS](https://aws.amazon.com/sqs/)). See Backup and Recovery suggested deployment scenarios.

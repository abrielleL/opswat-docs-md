<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/installation/aws-deployment -->

# AWS Deployment

This Deployment Guide provides step-by-step instructions for deploying MetaDefender Storage Security on Amazon Web Services (AWS) infrastructure.

This guide is intended for IT infrastructure architects, administrators, and DevOps professionals seeking to prevent malicious traffic from entering their AWS Cloud environment. It outlines how MetaDefender Core enhances threat prevention by inspecting uploaded productivity files and identifying known vulnerabilities in running services, applications, and unpatched operating systems deployed within AWS.

MetaDefender is provided in the following formats:

- An Amazon Machine Image (AMI) available through the AWS Marketplace ([MetaDefender products](https://aws.amazon.com/marketplace/seller-profile?id=1d722262-54b5-4258-b5fc-d01324b7a416)) (Recommended for PoC)
- A packaged installer available for download from the [My OPSWAT](https://my.opswat.com/) portal.
- Helm charts for MetaDefender products on [GitHub](https://github.com/OPSWAT/metadefender-k8s) with corresponding container images accessible from the [OPSWAT Docker Hub Repository](https://hub.docker.com/u/opswat)

Currently, there are no restrictions on the AWS regions where MetaDefender can be deployed, with the exception that MetaDefender is not available in AWS GovCloud at this time.

For installing our solution, please review the guidelines listed below to deploy the different infrastructure needed to install the product:

- [Deploy using EC2 Instances](/docs/mdicap/v5.14.1/installation/deploy-using-ec2-instances)
- [Deployment on EKS](/docs/mdicap/v5.14.1/installation/deployment-on-eks)

Database Configuration

MetaDefender Storage Security currently supports AWS RDS, an AWS-managed service compatible with PostgreSQL.

## [EC2 Key Management](/docs/mdicap/v5.14.1/installation/aws-deployment#ec2-key-management)

An EC2 key pair is used exclusively for SSH or RDP access to an EC2 instance, a scenario typically reserved for debugging.

You can either create a new key pair or use an existing one.

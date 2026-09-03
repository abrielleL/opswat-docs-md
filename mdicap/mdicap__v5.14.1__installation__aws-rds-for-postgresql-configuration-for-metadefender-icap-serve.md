<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve -->

# AWS RDS for PostgreSQL Configuration

### [Support AWS Services with PostgreSQL Engines](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#support-aws-services-with-postgresql-engines)

MetaDefender ICAP Server natively supports AWS RDS and Aurora with PostgreSQL engines up to 15.8 and 14.x**.** MetaDefender ICAP Server does not require any specific pre-installation steps to work with Amazon RDS - all required extensions are performed internally during installation of the product.

Regarding Aurora support, as it generates 2 endpoints, **Cluster endpoint** for administrate, insert and read. And the **reader endpoint** that is only for reading using the LB that get the information from any instance of the cluster. MetaDefender ICAP Server only supports connections to 1 endpoint, the cluster endpoint, that allow the application do all the actions needed. [Info from AWS](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.Endpoints.html#Aurora.Endpoints.Viewing)

## [Database Configuration](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#database-configuration)

### [High Availability with AWS RDS](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#high-availability-with-aws-rds)

AWS RDS supports various multi-az deployment that can be configured following [this documentation.](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/create-multi-az-db-cluster.html) You can compare the different configuration options available in [this AWS documentation](https://aws.amazon.com/rds/features/multi-az/). For having MetaDefender ICAP Server installed using any of this approaches we recommend to follow the instructions indicated by AWS in case of having ICAP installed in a EC2 instance. For EKS Cluster deployment OPSWAT provide a terraform code to deploy it together with the K8S cluster, see [EKS Cluster Provisioning](https://www.opswat.com/docs/mdcore/v5.14.1/cloud-deployment/eks-cluster-provision)

### [Database Sizing](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#database-sizing)

It depends on how many requests or traffic is sent to MetaDefender ICAP Server, and how complex the files are. As average the minimum database size desired **for each 1,000,000 analysis reports** added is **4.5GB.**

The recommended AWS RDS Instance Type is **db.r6g.xlarge** and the storage type recommended is General Purpose SSD. For gp2 storage type **the minimum size is 20 GiB** so this is marking as the minimum storage needed for working with MetaDefender ICAP Server

### [Security Group Configuration](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#security-group-configuration)

MetaDefender ICAP Server does not require that the RDS database is publicly accessible. For enhanced security, OPSWAT recommends the following:

- Do NOT deploy the database in a public subnet.
- Do NOT include ingress security group rules with 0.0.0.0/0 sources
- Do NOT set the Amazon RDS Publicly Accessible parameter to true in terraform project for Kubernetes deployment

## [Database Connection](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#database-connection)

For general information of how to connect to the RDS depending on the scenarios it is recommended to read this [docs from AWS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.Scenarios.html)

### [Connect to RDS in Private Subnet](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#connect-to-rds-in-private-subnet)

To connect MetaDefender ICAP Server with RDS hosted in a private subnet, the configuration will depend on the type of deployment.

**For Single EC2 deployment,** it is needed to indicate that the RDS will be only available from the EC2 instance where MetaDefender ICAP Server is running, configuring it from the Connectivity section when creating the RDS instance as following.

**For EKS deployment,** using the terraform project provided by OPSWAT it is deployed in a private subnet only allowing access from VPC CIDR where the EKS cluster is deployed. In case of creating the RDS instance from the console follow these steps

1. Indicate if you want to deploy it in Multi-AZ or Single DB

2. Indicate not to connect to an EC2 and the VPC public access "No". For multiple VPC, deploy it in a different VPC than EKS. This example is using the same VPC

### [Multiple VPC for MetaDefender ICAP Server and AWS RDS](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#multiple-vpc-for-metadefender-icap-server-and-aws-rds)

When working with multiple VPCs where we have deployed MetaDefender ICAP Server either in a Single EC2 or with EKS in one VPC and the RDS instance in a different VPC, it will be needed to configure a VPC peering between both VPC for MetaDefender ICAP Server to use the database.

Steps to configure it

1. Create a Peering Connection between both VPCs
2. Modify the route table to route the traffic to the peering for the requests from both VPCs
3. Modify the security group to allow connections from both VPCs

### [Database Endpoint Management](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#database-endpoint-management)

The database connection endpoint is generated by AWS once the RDS instance is created you can access to this information on the **Connectivity & security** tab. Once you have this information it should be set up in the ConfigMap "**mdicapsrv -env",** setting up the hostname of the database to DB_HOST and the port to DB_PORT

More detailed information from AWS [here](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_CommonTasks.Connect.html)

## [Database Encryption](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#database-encryption)

### [Database Encryption In Transit](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#database-encryption-in-transit)

Network traffic processed by MetaDefender ICAP Server is SSL encrypted during transmission. The product does not collect or store any customer data outside of analyzing the contents of files submitted for scanning.

During the scanning process, files are stored unencrypted on disk to allow the scan process to complete. Once the scan completes, the file is deleted unless configured to place the file in quarantine. If you wish to encrypt these quarantined files, please use native OS encryption or EBS encrypted volumes.

#### [Database Encryption At Rest](/docs/mdicap/v5.14.1/installation/aws-rds-for-postgresql-configuration-for-metadefender-icap-serve#database-encryption-at-rest)

MetaDefender ICAP Server supports both native OS encryption or EBS encrypted volumes. The database is secured via credentials and can be configured to encrypt everything at rest. In general, OPSWAT recommends the use of a 3rd party database layer, e.g. Amazon Aurora or RDS, which should be encrypted. It is best practice to not share the database layer on the same hosts/VM/EC2 instance.

For encrypting RDS this is the recommended configuration

More info

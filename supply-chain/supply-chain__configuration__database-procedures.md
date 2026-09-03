<!-- source: https://www.opswat.com/docs/supply-chain/configuration/database-procedures -->

# AWS RDS with PostgreSQL

#### [Support AWS Services with PostgreSQL Engines](https://www.opswat.com/docs/mdss/configuration/documentdb-support#support-aws-services-with-postgresql-engines)

MetaDefender Software Supply-Chain natively supports AWS RDS and Aurora with PostgreSQL engine**.** MetaDefender Software Supply-Chain does not require any specific pre-installation steps to work with Amazon RDS - all required extensions are performed internally during installation of the product.

Regarding Aurora support, as it generates 2 endpoints, **Cluster endpoint** for administrate, insert and read. And the **reader endpoint** that is only for reading using the LB that get the information from any instance of the cluster. MetaDefender Software Supply-Chain only supports connections to 1 endpoint, the cluster endpoint, that allow the application do all the actions needed. [Info from AWS](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.Endpoints.html#Aurora.Endpoints.Viewing)

You can create and configure AWS RDS and PostgreSQL by following the guide [here.](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.PostgreSQL.html)

## [Database Configuration](https://www.opswat.com/docs/mdss/configuration/documentdb-support#database-configuration)

### [High Availability with AWS RDS](https://www.opswat.com/docs/mdss/configuration/documentdb-support#high-availability-with-aws-rds)

AWS RDS supports various multi-az deployment that can be configured following [this documentation.](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/create-multi-az-db-cluster.html) You can compare the different configuration options available in [this AWS documentation](https://aws.amazon.com/rds/features/multi-az/). For having MetaDefender Software Supply-Chain installed using any of this approaches we recommend to follow the instructions indicated by AWS in case of having MDSSC installed in a EC2 instance. For EKS Cluster deployment OPSWAT provide a terraform code to deploy it together with the K8S cluster, see [EKS Cluster Provisioning](https://www.opswat.com/installation/deployment-on-eks)

### [Database Sizing](https://www.opswat.com/docs/mdss/configuration/documentdb-support#database-sizing)

It depends on how many requests or traffic is sent to MetaDefender Software Supply-Chain, and how complex the files are. As average the minimum database size desired **for each 1,000,000 analysis reports** added is **6 GB.**

The recommended AWS RDS Instance Type is **db.r6g.xlarge** and the storage type recommended is General Purpose SSD. For gp2 storage type **the minimum size is 20 GiB** so this is marking as the minimum storage needed for working with MetaDefender Storage Security.

### [Security Group Configuration](https://www.opswat.com/docs/mdss/configuration/documentdb-support#security-group-configuration)

MetaDefender Software Supply-Chain does not require that the RDS database is publicly accessible. For enhanced security, OPSWAT recommends the following:

- Do NOT deploy the database in a public subnet.
- Do NOT include ingress security group rules with 0.0.0.0/0 sources
- Do NOT set the Amazon RDS Publicly Accessible parameter to true in terraform project for Kubernetes deployment

## [Database Connection](https://www.opswat.com/docs/mdss/configuration/documentdb-support#database-connection)

For general information of how to connect to the RDS depending on the scenarios it is recommended to read this [docs from AWS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.Scenarios.html).

### [Connect to RDS in Private Subnet](https://www.opswat.com/docs/mdss/configuration/documentdb-support#connect-to-rds-in-private-subnet)

To connect MetaDefender Software Supply-Chain with RDS hosted in a private subnet, the configuration will depend on the type of deployment.

**For Single EC2 deployment,** it is needed to indicate that the RDS will be only available from the EC2 instance where MetaDefender Software Supply-Chain is running, configuring it from the Connectivity section when creating the RDS instance as following.

**For EKS deployment,** using the terraform project provided by OPSWAT it is deployed in a private subnet only allowing access from VPC CIDR where the EKS cluster is deployed. In case of creating the RDS instance from the console follow these steps

1. Indicate if you want to deploy it in Multi-AZ or Single DB

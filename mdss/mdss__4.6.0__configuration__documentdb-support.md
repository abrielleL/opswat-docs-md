<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/documentdb-support -->

# AWS RDS with PostgreSQL

### Support AWS Services with PostgreSQL Engines

MetaDefender Storage Security natively supports AWS RDS and Aurora with PostgreSQL engine ([Supported PostgreSQL versions](https://www.opswat.com/docs/mdss/getting-started/general-system-requirements))**.** MetaDefender Storage Security does not require any specific pre-installation steps to work with Amazon RDS - all required extensions are performed internally during installation of the product.

Regarding Aurora support, as it generates 2 endpoints, **Cluster endpoint** for administrate, insert and read. And the **reader endpoint** that is only for reading using the LB that get the information from any instance of the cluster. MetaDefender Storage Security only supports connections to 1 endpoint, the cluster endpoint,  that allow the application do all the actions needed. [Info from AWS](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.Endpoints.html#Aurora.Endpoints.Viewing)

You can create and configure AWS RDS and PostgreSQL by following the guide [here.](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.PostgreSQL.html)

## Database Configuration

### High Availability with AWS RDS

AWS RDS supports various multi-az deployment that can be configured following [this documentation.](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/create-multi-az-db-cluster.html) You can compare the different configuration options available in [this AWS documentation](https://aws.amazon.com/rds/features/multi-az/). For having MetaDefender Storage Security installed using any of this approaches we recommend to follow the instructions indicated by AWS in case of having MDSS installed in a EC2 instance. For EKS Cluster deployment OPSWAT provide a terraform code to deploy it together with the K8S cluster, see [Deployment on EKS](https://www.opswat.com/docs/mdss/installation/deployment-on-eks)

### Database Sizing

It depends on how many requests or traffic is sent to MetaDefender Storage Security, and how complex the files are. As average the minimum database size desired **for each 1,000,000 analysis reports** added is **6 GB.**

The recommended AWS RDS Instance Type is **db.r6g.xlarge** and the storage type recommended is General Purpose SSD. For gp2 storage type **the minimum size is 20 GiB** so this is marking as the minimum storage needed for working with MetaDefender Storage Security.

### Security Group Configuration

MetaDefender Storage Security does not require that the RDS database is publicly accessible. For enhanced security, OPSWAT recommends the following:

- Do NOT deploy the database in a public subnet.
- Do NOT include ingress security group rules with 0.0.0.0/0 sources
- Do NOT set the Amazon RDS Publicly Accessible parameter to true in terraform project for Kubernetes deployment

## Database Connection

For general information of how to connect to the RDS depending on the scenarios it is recommended to read this [docs from AWS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.Scenarios.html).

### Connect to RDS in Private Subnet

To connect MetaDefender Storage Security with RDS hosted in a private subnet, the configuration will depend on the type of deployment.

**For Single EC2 deployment,** it is needed to indicate that the RDS will be only available from the EC2 instance where MetaDefender Storage Security is running, configuring it from the Connectivity section when creating the RDS instance as following.

![](https://uploads.developerhub.io/prod/k8zL/8e6eaoaht8f91prijguhuwpvnaibxjk7o84i90nxe43f98h43fpbkumub1n3dtd4.png)

**For EKS deployment,** using the terraform project provided by OPSWAT it is deployed in a private subnet only allowing access from VPC CIDR where the EKS cluster is deployed. In case of creating the RDS instance from the console follow these steps

1. Indicate if you want to deploy it in Multi-AZ or Single DB

![](https://uploads.developerhub.io/prod/k8zL/i03mbkjhofw4hxji3irdybyhd3rivtkd8ccd182odrsyili0y3abehwcmqlrphn4.png)

2. Indicate not to connect to an EC2 and the VPC public access "No". For multiple VPC, deploy it in a different VPC than EKS. This example is using the same VPC

![](https://uploads.developerhub.io/prod/k8zL/8fkvs2z8c4z4jn2xnk51mill3j56b2ftk8gaaokcbnzcuzcowbvo5e6op8a26ppv.png)

### Multiple VPC for MetaDefender Storage Security and AWS RDS

When working with multiple VPCs where we have deployed MetaDefender Storage Security either in a Single EC2 or with EKS in one VPC and the RDS instance in a different VPC, it will be needed to configure a VPC peering between both VPC for MetaDefender Storage Security to use the database.

Steps to configure it

1. Create a Peering Connection between both VPCs
2. Modify the route table to route the traffic to the peering for the requests from both VPCs
3. Modify the security group to allow connections from both VPCs

### Database Endpoint Management

The database connection endpoint is generated by AWS once the RDS instance is created you can access to this information on the **Connectivity & security** tab. Once you have this information it should be set up in the `ConfigMap` , configuring the hostname of the database and the port to match the new RDS instance.

More detailed information from AWS [here](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_CommonTasks.Connect.html).

## Database Encryption

MetaDefender Storage Security supports both native OS encryption or EBS encrypted volumes. The database is secured via credentials and can be configured to encrypt everything at rest. In general, OPSWAT recommends the use of a 3rd party database layer, e.g. Amazon Aurora or RDS, which should be encrypted. It is best practice to not share the database layer on the same hosts/VM/EC2 instance.

For encrypting RDS this is the recommended configuration

![](https://uploads.developerhub.io/prod/k8zL/4yxazac6idwjfyshkckz8lnt8m5szcfg3krjquwv0f98u4co7urr8c7gejiiff9r.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

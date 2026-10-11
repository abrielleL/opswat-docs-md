<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/cloud-deployment/single-ec2-architecture -->

# Single EC2

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The single instance deployment is only recommended for small or test environments that do not need high availability. This deployment consist of a AWS EC2 instance using the MetaDefender Core AMI published in the marketplace that includes a Standalone MetaDefender Core where the PostgreSQL database is deployed in the same instance than MetaDefender Core.

## [Diagram](/docs/mdcore/v5.22.1/cloud-deployment/single-ec2-architecture#diagram)

#### [Orange flows](/docs/mdcore/v5.22.1/cloud-deployment/single-ec2-architecture#orange-flows)

- **A**: From a private subnet, client is getting the files and uploading them to MetaDefender Core using the **private IP**
- **B**: From Internet, client is outside the VPC and is sending files to MetaDefender Core using the **public IP**

#### [Blue flows](/docs/mdcore/v5.22.1/cloud-deployment/single-ec2-architecture#blue-flows)

- MetaDefender Core get activated and updates the modules installed on it after activation

This diagram show the standalone database option where the analysis results are stored.

## [Resources Inventory](/docs/mdcore/v5.22.1/cloud-deployment/single-ec2-architecture#resources-inventory)

### [Access Management](/docs/mdcore/v5.22.1/cloud-deployment/single-ec2-architecture#access-management)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| IAM Role | LambdaAccessRole | Role for Lambdas |
| IAM Role | LambdaExecutionRole | Role with Policy for logging |
| IAM Instance Profile | LambdaInstanceProfile | IAM InstanceProfile that is attached to the EC2 instance |
| IAM Policy | lambdaaccess | Policy attached to LambdaAccessRole for allowing all lambda and and events actions. |
| AWS Lambda Permissions | PermissionForEventsToInvokeLambda | Lambda Permission needed to invoke the DeactivateLambda function |

### [Networking](/docs/mdcore/v5.22.1/cloud-deployment/single-ec2-architecture#networking)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| VPC | <VPC Name> (parameter) | Desired Virtual Private Cloud |
| Subnet | terraform-${var.ENV_NAME}/SubnetPublicX | Desired Public Subnet |
| Subnet | terraform-${var.ENV_NAME}/SubnetPrivateX | Desired PrivateSubnet |
| Internet Gateway | terraform-${var.ENV_NAME}/InternetGateway | Internet Gateway for VPC |
| Elastic IP | terraform-${var.ENV_NAME}/NATIP | Public IP for NAT Gateway |
| NAT Gateway | terraform-${var.ENV_NAME}/NATGateway | NAT Gateway to give access to internet from private subnet |
| Route Table | terraform-${var.ENV_NAME}/PublicRouteTable | Route Table for Public Subnet |
| Route Table | terraform-${var.ENV_NAME}/PrivateRouteTable | Route Table for Private Subnet |

### [Security](/docs/mdcore/v5.22.1/cloud-deployment/single-ec2-architecture#security)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Security Group | MetaDefenderSecurityGroup | Generated security group to allow traffic to MetaDefender REST API. |

### [Compute](/docs/mdcore/v5.22.1/cloud-deployment/single-ec2-architecture#compute)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| EC2 Instance | ${var.ENV__NAME}-${var.APP_ _NAME}-instance | Instance to run MetaDefender Core AMI |
| Launch Template | ${var.APP_NAME}-template | Launch Template for MetaDefender Instance |

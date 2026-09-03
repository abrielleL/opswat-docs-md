<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/cloud-deployment/autoscaling-ec2-architecture -->

# Autoscaling EC2

The autoscaling deployment is the recommended deployment for production environments that need high availability. This deployment consist of an AWS Auto-Scaling Group (ASG in this page from now on) with instances using the MetaDefender Core AMI published in the AWS marketplace that includes a Standalone MetaDefender Core where the PostgreSQL database is deployed in the same instance than MetaDefender Core.

## [Only MetaDefender Core Diagram](/docs/mdcore/v5.21.0/cloud-deployment/autoscaling-ec2-architecture#only-metadefender-core-diagram)

There are 2 flows for MetaDefender Core to work

- **Orange Flow**: Flow to scan a file from internet hitting the network load balancer that is before the autoscaling group. There are other options for sending files to scan, like do it from a private subnet or through a VPN or any other mechanism to hit the network load balancer that is the point to send the request to the MetaDefender Core instances.
- To control the instances **activation**.

  - (**Default/Recommended**) Passing LICENSE_KEY and APIKEY as environment variables through the user-data. The MetaDefender Core instance will activate the instance on start and deactivate it on shutdown.
  - **(Optional) Black Flow**: The lambda function is triggered based on the ASG events. On activation this flow joins with **blue flow,** the lambda function stores the licensing information in the parameter store.

    - When instance **new in ASG,** Core is activated and instance **started**
    - When instance moved from **ASG to Warm Pool**, Core is deactivated on Scale down and instance **stopped**
    - When instance **new in Warm Pool** ASG, Core is left deactivated and instance stopped
    - When instance move from **Warm Pool ASG to ASG**, instance is **started** and Core is activated
- **Blue Flow**: Each instance communicates with OPSWAT to activate/deactivate and update the AV engines. In case of using lambda function activation, the deactivation happens between the Lambda function and OPSWAT.

## [MetaDefender Core and MetaDefender ICAP Server Diagram](/docs/mdcore/v5.21.0/cloud-deployment/autoscaling-ec2-architecture#metadefender-core-and-metadefender-icap-server-diagram)

Example of the recommended architecture for MetaDefender Core and MetaDefender ICAP Server running in ASG.

## [Resources Inventory](/docs/mdcore/v5.21.0/cloud-deployment/autoscaling-ec2-architecture#resources-inventory)

### [Access Management](/docs/mdcore/v5.21.0/cloud-deployment/autoscaling-ec2-architecture#access-management)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| IAM Role | LambdaAccessRole | Role for Lambdas |
| IAM Role | LambdaExecutionRole | Role with Policy for logging |
| IAM Instance Profile | LambdaInstanceProfile | IAM InstanceProfile that is attached to the EC2 instance |
| IAM Policy | lambdaaccess | Policy attached to LambdaAccessRole for allowing all lambda and and events actions. |
| AWS Lambda Permissions | PermissionForEventsToInvokeLambda | Lambda Permission needed to invoke the DeactivateLambda function |

### [Networking](/docs/mdcore/v5.21.0/cloud-deployment/autoscaling-ec2-architecture#networking)

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

### [Security](/docs/mdcore/v5.21.0/cloud-deployment/autoscaling-ec2-architecture#security)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Security Group | MetaDefenderSecurityGroup | Generated security group to allow traffic to MetaDefender REST API. |

### [Compute](/docs/mdcore/v5.21.0/cloud-deployment/autoscaling-ec2-architecture#compute)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| EC2 Instance | ${var.ENV__NAME}-${var.APP_ _NAME}-instance | Instance to run MetaDefender Core AMI |
| Launch Template | ${var.APP_NAME}-template | Launch Template for MetaDefender Instance |

<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/cloud-deployment/recommended-architectures-in-aws -->

# Recommended Architectures

This page explains the recommended architecture for running MetaDefender Core in an AWS EC2 instance or AWS EKS (Kubernetes)

## [Infrastructure Options for MetaDefender Core in AWS EC2](/docs/mdcore/v5.22.0/cloud-deployment/recommended-architectures-in-aws#infrastructure-options-for-metadefender-core-in-aws-ec2)

The possible infrastructure options vary depending on the number of EC2 instances where MetaDefender Core will be installed.

Options:

1. [Single EC2](/docs/mdcore/v5.22.0/cloud-deployment/single-ec2-architecture)
2. [Autoscaling EC2](/docs/mdcore/v5.22.0/cloud-deployment/autoscaling-ec2-architecture)

## [Infrastructure Options for MetaDefender Core in AWS EKS](/docs/mdcore/v5.22.0/cloud-deployment/recommended-architectures-in-aws#infrastructure-options-for-metadefender-core-in-aws-eks)

The possible infrastructure options vary depending on the AWS services used to host MetaDefender Core and how the PostgreSQL database is provisioned.

Options:

1. EKS Cluster with **EC2 Instances + AWS RDS**
2. EKS Cluster with **EC2 Instances + PostgreSQL Pod**
3. EKS Cluster with **AWS Fargate + PostgreSQL Pod**
4. EKS Cluster with **AWS Fargate + AWS RDS**

The above options are explained in [EKS Cluster Architecture](/docs/mdcore/v5.22.0/cloud-deployment/eks-cluster-architecture)

We offer a provisioning script that, depending on the selection, automatically provisions the cluster for you and installs the K8S components needed for the MetaDefender Core service. See [EKS Cluster Deployment](/docs/mdcore/v5.22.0/cloud-deployment/eks-cluster-provision)

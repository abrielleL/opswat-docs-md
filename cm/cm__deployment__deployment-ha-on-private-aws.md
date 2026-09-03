<!-- source: https://www.opswat.com/docs/cm/deployment/deployment-ha-on-private-aws -->

# Deployment High Availability on AWS

## Purpose

Give operators a concise, end-to-end view of the MOCM on‑prem deployment on AWS, with links to the detailed guides, expected inputs/outputs per step, and a post-deploy validation checklist.

## Prerequisites (high-level)

- AWS account with permissions for VPC, EKS, EC2, S3, Amazon MQ, ElastiCache, ACM, and Route 53
- Local tooling installed: OpenTofu/Terraform, AWS CLI, kubectl, Helm, Helmfile, jq
- Access to the MOCM on‑prem deployment package (Terraform modules, Ansible roles, Helm charts, images)

> **Important**
>
> Ensure network egress and IAM permissions allow provisioning of required resources and SSM connectivity for configuration steps.

## Deployment workflow (2 steps)

### Step 1 – Deploy Infrastructure (AWS)

Goal: Provision the foundational cloud resources to run MOCM.

- Core networking: VPC, subnets, NAT, VPC endpoints
- EKS cluster, node groups, and ALB ingress controller
- Data services: MongoDB (via Ansible over SSM), Amazon MQ (RabbitMQ), Redis (ElastiCache), S3 buckets
- DNS and certificates: Route 53 hosted zone and ACM certificate

Guide: [Deploy Infrastructure (AWS)](https://www.opswat.com/docs/cm/deployment/deploy-infra-for-private-cloud-aws)

#### Expected outputs from Step 1 (hand‑off to Step 2)

- EKS cluster reachable with kubectl (cluster name and region known)
- Application DNS hostnames reserved and ACM certificate issued/validated
- MongoDB replica set endpoints and credentials are ready
- RabbitMQ (Amazon MQ) and Redis endpoints are available
- S3 buckets and prefixes for object storage are configured

### Step 2 – Deploy Application (Helm Charts)

Goal: Install and configure MOCM services onto the provisioned EKS cluster.

- Push container images to your registry (e.g., ECR)
- Populate values in Helm charts (hosts, credentials, storage, scaling)
- Deploy with Helm/Helmfile and verify pods, services, and ingress

Guide: [Deploy Application with Helm Charts](https://www.opswat.com/docs/cm/deployment/deploy-application-with-helm-charts)

## Where to find required values

- OpenTofu/Terraform outputs: cluster name, VPC/network, data service endpoints, S3 bucket names
- AWS Secrets Manager: credentials (MongoDB, RabbitMQ, Redis), application secrets, TLS private keys if managed there

> **Tip**
>
> Keep a single hand-off record that maps Terraform outputs to Helm values (e.g., endpoints, ports, database names). This reduces misconfiguration and accelerates Step 2.

## Post-deploy validation checklist

- DNS and Certificates: Domain resolves to the ingress load balancer; ACM certificate shows issued and is attached to the ingress
- Ingress/Networking: Ingress resources exist; ALB/NGINX shows healthy targets; security groups allow traffic from clients
- Cluster Health: kubectl shows all pods in Running/Ready; no CrashLoopBackOff; node capacity sufficient for default replicas
- UI Access: Browse to the configured hostname over HTTPS and log in successfully
- Smoke Checks: Core API endpoints respond 2xx; background jobs/processors start; storage interactions (S3) succeed

<!-- source: https://www.opswat.com/docs/mdss/4.4.2/installation/azure-deployment -->

# Azure Deployment

### [Introduction](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#introduction)

This Deployment Guide provides step-by-step instructions for deploying MetaDefender Storage Security on Azure Cloud Services infrastructure.

This guide is for IT infrastructure architects, administrators and DevOps professionals who are seeking to prevent potential malicious traffic being allowed in their Azure Cloud deployment. Threat Prevention is ensured for both productivity files that might be uploaded and for known vulnerabilities that can be identified for all running services/applications deployed in Azure. The vulnerability scanning is checking known vulnerabilities for unpatched OS and running applications.

MetaDefender is provided as:

- AMI through the Azure Marketplace ([MetaDefender products](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=MetaDefender&page=1))
- A packaged installer available for download from the [My OPSWAT](https://my.opswat.com/) portal.
- Helm charts for MetaDefender products on [GitHub](https://github.com/OPSWAT/metadefender-k8s) with corresponding container images accessible from the [OPSWAT Docker Hub Repository](https://hub.docker.com/u/opswat)

There are currently no restrictions on Azure regions in which you can deploy MetaDefender. The only restriction is that MetaDefender is not available Azure for Government at this time.

For deploying our solution in Azure, please review the guideline listed below:

- [Deploy using Azure VMs](/docs/mdss/4.4.2/installation/deploy-using-azure-vms)
- [Deployment on AKS](/docs/mdss/4.4.2/installation/deployment-on-aks)

### [Private Key Management](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#ec2-key-management)

The Private key pair is only used to SSH or RDP to the Azure VM. This is a very uncommon scenario, used primarily for debugging. You can create a new key pair, or use an existing pair.

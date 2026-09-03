<!-- source: https://www.opswat.com/docs/mdss/4.4.2/installation/gcp-deployment -->

# GCP Deployment

### [Introduction](https://docs.opswat.com/mdcore/cloud-deployment/aws-deployments#introduction)

This Deployment Guide provides step-by-step instructions for deploying MetaDefender Storage Security on Google Cloud Services infrastructure.

This guide is for IT infrastructure architects, administrators and DevOps professionals who are seeking to prevent potential malicious traffic being allowed in their Google Cloud deployment. Threat Prevention is ensured for both productivity files that might be uploaded and for known vulnerabilities that can be identified for all running services/applications deployed in Google. The vulnerability scanning is checking known vulnerabilities for unpatched OS and running applications.

MetaDefender is provided as:

- A packaged installer available for download from the [My OPSWAT](https://my.opswat.com/) portal.
- Helm charts for MetaDefender products on [GitHub](https://github.com/OPSWAT/metadefender-k8s) with corresponding container images accessible from the [OPSWAT Docker Hub Repository](https://hub.docker.com/u/opswat)
- AMI through the Google Marketplace (**On Roadmap for Storage Security, for MetaDefender Core it is available**)

There are currently no restrictions on Google regions in which you can deploy MetaDefender.

For deploying our solution in Google, please review the guideline listed below:

- [Deploy using Google Compute Engines](/docs/mdss/4.4.2/installation/deploy-using-google-compute-engines)
- [Deployment on GKE](/docs/mdss/4.4.2/installation/deployment-on-gke)

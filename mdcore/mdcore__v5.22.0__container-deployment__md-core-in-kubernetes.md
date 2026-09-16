<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/container-deployment/md-core-in-kubernetes -->

# Overview

## [Introduction](/docs/mdcore/v5.22.0/container-deployment/md-core-in-kubernetes#introduction)

This Installation Guide provides step-by-step instructions for installing MetaDefender Core in your own Kubernetes cluster in whatever environment you have it deployed.

Organizations interested in protecting their solutions deployed in Kubernetes technology can leverage MetaDefender to analyze and sanitize files. MetaDefender can scan and either sanitize or check for known vulnerabilities, depending on the type of traffic it's seeing. Analyzing files before they are made accessible to the end-users is critical to ensure that no malicious content is allowed and distributed through the web application.

This guide is for IT infrastructure architects, administrators and DevOps professionals who are seeking to prevent potential malicious traffic being allowed in their environments. Threat Prevention is ensured for both productivity files that might be uploaded and for known vulnerabilities that can be identified for all running services/applications. The vulnerability scanning is checking known vulnerabilities for unpatched OS and running applications.

#### [Guide Structure](/docs/mdcore/v5.22.0/container-deployment/md-core-in-kubernetes#guide-structure)

1. [Kubernetes Components](/docs/mdcore/v5.22.0/container-deployment/kubernetes-components)
2. [Deploying on K8S](/docs/mdcore/v5.22.0/container-deployment/deployment-strategies-kubernetes)
3. [Upgrade/Deployment Strategy on K8S](/docs/mdcore/v5.22.0/container-deployment/upgrade-metadefender-core-version-on-k8s)
4. [High Availability on K8S](/docs/mdcore/v5.22.0/container-deployment/high-availability-on-k8s)
5. [Scaling K8S Cluster](/docs/mdcore/v5.22.0/container-deployment/scaling-k8s-cluster)
6. [Troubleshooting](/docs/mdcore/v5.22.0/container-deployment/troubleshooting)

## [Kubernetes Supported Versions](/docs/mdcore/v5.22.0/container-deployment/md-core-in-kubernetes#kubernetes-supported-versions)

| Kubernetes Version | Known Limitations |
| --- | --- |
| 1.22.17 and later | None |
| Before 1.22.17 | When pod eviction, automation of core deactivation fails. |

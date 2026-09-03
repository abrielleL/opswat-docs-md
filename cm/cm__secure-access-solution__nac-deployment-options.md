<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/nac-deployment-options -->

# Deployment Options

MetaDefender NAC v10 supports hybrid and on-premises deployment models. Choose a model based on where you want to host the management console and your organization's operational and security requirements.

## Compare Hybrid NAC and On-premise NAC

| Deployment consideration | Hybrid NAC | On-premise NAC |
| ---- | ---- | ---- |
| **Management console** | Cloud-hosted My OPSWAT Central Management | My OPSWAT Central Management hosted in your environment |
| **Network enforcement** | A NAC Edge VM deployed on the local network communicates directly with network devices and receives configuration and policy updates from the cloud. | A NAC VM deployed on the local network communicates directly with network devices and is registered to the on-premises My OPSWAT Central Management instance. |
| **Administration** | Centralized cloud management with local enforcement at one or more sites | Management and enforcement remain within the organization's environment |
| **Best suited for** | Organizations that want OPSWAT-hosted management while keeping direct communication with network devices on-site | Organizations that need to host the management plane and NAC components in their own environment |

## Hybrid NAC

[Hybrid NAC](https://www.opswat.com/docs/cm/secure-access-solution/hybrid-nac) combines a cloud-hosted My OPSWAT Central Management console with one or more NAC Edge VMs deployed in your environment. Each NAC Edge communicates directly with local network devices to enforce access policies while receiving configuration and policy updates from the cloud.

Hybrid NAC supports multi-site deployments. You can deploy a NAC Edge at each site and centrally monitor the deployed Edges from My OPSWAT Central Management. Each NAC Edge requires a dedicated VM.

Choose Hybrid NAC when you want:

- Cloud-hosted administration and centralized visibility.
- Local policy enforcement and communication with network devices.
- Independent NAC Edge deployments across multiple sites.
- Less on-premises management infrastructure than a fully on-premises deployment.

Before deployment, review the [Hybrid NAC technical requirements](https://www.opswat.com/docs/cm/secure-access-solution/technical-requirements) and then [download and install the NAC Edge VM](https://www.opswat.com/docs/cm/secure-access-solution/deployment-for-hybrid).

## On-premise NAC

[On-premise NAC](https://www.opswat.com/docs/cm/secure-access-solution/on-premise-nac) hosts both My OPSWAT Central Management and the NAC VM within your environment. The local NAC component communicates directly with network devices and receives its configuration from your self-hosted My OPSWAT Central Management instance.

Choose On-premise NAC when you want:

- The management console and NAC components hosted in your environment.
- Direct control over the infrastructure that provides NAC management and enforcement.
- A deployment model that does not rely on the cloud-hosted My OPSWAT Central Management console.

An on-premises deployment requires you to deploy My OPSWAT Central Management in addition to the NAC VM. Before deployment, review the [On-premise NAC technical requirements](https://www.opswat.com/docs/cm/secure-access-solution/technical-requirements-onprem) and then [install My OPSWAT Central Management and the NAC VM](https://www.opswat.com/docs/cm/secure-access-solution/deployment-for-on-premise).

## Choose a deployment model

Select **Hybrid NAC** if cloud-hosted management is acceptable and you want local enforcement close to your network devices. Select **On-premise NAC** if your organization must host and operate both the management console and NAC infrastructure.

Also consider your available virtualization resources, connectivity requirements, number of sites, and internal requirements for data location and infrastructure ownership before choosing a model.

<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-compatibility-matrix -->

# MetaDefender Cluster Compatibility Matrix

## [Benefits of MetaDefender Cluster](/docs/mdcluster/installation/md-cluster-compatibility-matrix#benefits-of-metadefender-cluster)

By integrating with MetaDefender Cluster (MD Cluster), administrators can take advantage of simplified scalability, high availability, distributed extraction, and improved performance optimization — all through a single, unified MD Cluster API Gateway endpoint.

## [Version Compatibility Matrix](/docs/mdcluster/installation/md-cluster-compatibility-matrix#version-compatibility-matrix)

The table below shows the minimum supported product versions compatible with MD Cluster version 2.6.0, running MetaDefender Core (MD Core) version 5.18.1.

| Product | Minimum Supported Version |
| --- | --- |
| MetaDefender Storage Security | 4.4.0 |
| MetaDefender Kiosk | 4.8.1 |
| MetaDefender Email Gateway Security | 6.3.2 |
| MetaDefender ICAP Server | 5.13.0 |
| MetaDefender Managed File Transfer | 3.11.3 |
| MetaDefender Software Supply Chain | 3.3.1 |
| MetaDefender Endpoint | 7.6.2605.999 |

## [Integration through MD Cluster API Gateway](/docs/mdcluster/installation/md-cluster-compatibility-matrix#integration-through-md-cluster-api-gateway)

To ensure seamless integration with MD Cluster, all products must communicate directly with **MD Cluster API Gateway** instead of connecting to individual MD Core instances.

All file scanning and result retrieval requests should be routed through MD Cluster API Gateway

1. [File analysis](https://www.opswat.com/docs/mdcluster/api-gateway#tag-analysis)
2. [Batch analysis](https://www.opswat.com/docs/mdcluster/api-gateway#tag-batch)
3. [Fetching scan results](https://www.opswat.com/docs/mdcluster/api-gateway#fileanalysisget)

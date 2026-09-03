<!-- source: https://www.opswat.com/docs/mdcluster/operating/md-cluster-workflow-management -->

# Workflow Management

This section explains how MetaDefender Cluster (MD Cluster) selects and applies scanning workflows based on client source IP addresses and REST API requests. It also describes how workflow rules determine scan processing behavior and validation.

## [How scan profiles are selected](/docs/mdcluster/operating/md-cluster-workflow-management#how-scan-profiles-are-selected)

MD Cluster can use different scanning profiles for different clients. The profile selection is based on the client’s source IP address.

If multiple scanning profiles are available for a client, the client can specify which profile to use in the request. If no profile is specified, MD Cluster applies the first matching profile defined in the Workflow rules.

## [How file scans are processed through the REST API](/docs/mdcluster/operating/md-cluster-workflow-management#how-file-scans-are-processed-through-the-rest-api)

When MD Cluster API Gateway receives a scan request through the REST API, it checks the client’s source IP address against the configured workflow rules. The first matching rule determines which workflow is applied to the scan request.

If the REST API request explicitly specifies a workflow, that workflow must also match an existing rule for the client. Otherwise, the scan request is rejected.

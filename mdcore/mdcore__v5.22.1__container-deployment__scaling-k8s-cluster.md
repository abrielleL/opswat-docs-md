<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster -->

# Scaling K8S Cluster

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Scaling up Cores](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#scaling-up-cores)

### [Flow Diagram](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#flow-diagram)

- Traffic won’t be sent to pods until readiness probe is successful

  - Readiness probe is using health check API to check that engines are ready.
- If we scale it down, older pods will be terminated

### [Command to Scale up](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#command-to-scale-up)

BashCopykubectl scale deployment md-core --replicas=<num_replicas>
## [Autoscaling MetaDefender Core](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#autoscaling-metadefender-core)

There are different levels and ways to auto-scale an application when running in a Kubernetes cluster.

- When autoscaling the pods running in the Kubernetes cluster it is needed to run the [Horizontal Pod AutoScaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/)
- To ensure that the Kubernetes cluster has enough nodes to schedule the pods to scale, it is recommended to use the [Kubernetes Cluster AutoScaler](https://aws.github.io/aws-eks-best-practices/cluster-autoscaling/).

### [Pre-requisites](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#pre-requisites)

- Kubernetes Cluster already deployed
- Kubernetes Metrics Server installed - [Installing the Kubernetes Metrics Server - Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/metrics-server.html)
- Kubectl client installed

### [Limitations](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#limitations)

- Manual scale get disabled by the HPA

### [Autoscaling Architecture on K8S Cluster](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#autoscaling-architecture-on-k8s-cluster)

In grey the components needed to be added to have a full autoscaling architecture with AWS as example.

### [Steps to install Horizontal Pod Autoscaler for Core](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#steps-to-install-horizontal-pod-autoscaler-for-core)

- Deploy HPA with kubectl

BashCopykubectl autoscale deployment md-core --cpu-percent=95 --min=1 --max=5
### [Steps to install Cluster Autoscaler (Manual Configuration)](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#steps-to-install-cluster-autoscaler-manual-configuration)

#### [Permissions](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#permissions)

Cluster Autoscaler requires the ability to examine and modify EC2 Auto Scaling Groups. We recommend using [IAM roles for Service Accounts](https://docs.aws.amazon.com/eks/latest/userguide/iam-roles-for-service-accounts.html) to associate the Service Account that the Cluster Autoscaler Deployment runs as with an IAM role that is able to perform these functions

For that it is needed to attach the following policy __[example_scripts/iam_policy_cluster_autoscaler.json](https://github.com/OPSWAT/metadefender-k8s/blob/main/example_scripts/iam_policy_cluster_autoscaler.json) to the service account with name `cluster-autoscaler`

#### [One ASG Setup](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#one-asg-setup)

Cluster Autoscaler can be configured manually if you wish by passing the `--nodes` argument at startup. The format of the argument is `--nodes=<min>:<max>:<asg-name>`, where `<min>` is the minimum number of nodes, `<max>` is the maximum number of nodes, and `<asg-name>` is the Auto Scaling Group name.

- Both `<min>` and `<max>` must be within the range of the minimum and maximum instance counts already specified by the Auto Scaling group.
- When manual configuration is used, the Auto Scaling groups must use EC2 instance types that provide equal CPU and memory capacity.

**It is needed to replace the following variables in** [**example_scripts/cluster-autoscaler-one-asg-aws.yaml**](https://github.com/OPSWAT/metadefender-k8s/blob/main/example_scripts/cluster-autoscaler-one-asg-aws.yaml) **before applying the changes <MIN_NODES>, <MAX_NODES> and <K8S_ASG_NAME>**

BashCopykubectl apply -f example_scripts/cluster-autoscaler-one-asg-aws.yaml
### [Script provided by OPSWAT with all Steps](/docs/mdcore/v5.22.1/container-deployment/scaling-k8s-cluster#script-provided-by-opswat-with-all-steps)

OPSWAT provides an [script](https://github.com/OPSWAT/metadefender-k8s/blob/main/example_scripts/install_hpa_and_cluster_autoscaler_aws.sh) that automatically replace all the variables from the files needed to create HPA and Cluster Autoscaler

BashCopycd example_scripts
install_hpa_and_cluster_autoscaler_aws.sh --min <min_nodes> --max <max_nodes> --region <asg_region> --cluster_name <cluster_name> --asg_name <k8s_asg_name> --account_id <aws_account_id>"

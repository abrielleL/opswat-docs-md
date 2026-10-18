<!-- source: https://www.opswat.com/docs/mdss/4.6.0/installation/kubernetes-deployment -->

# Kubernetes Deployment

This Installation Guide provides step-by-step instructions for installing MetaDefender Storage Security (MDSS) in your own Kubernetes cluster in whatever environment you have it deployed.

This guide is for IT infrastructure architects, administrators and DevOps professionals who are seeking to prevent potential malicious traffic being allowed in their environments. Threat Prevention is ensured for both productivity files that might be uploaded and for known vulnerabilities that can be identified for all running services/applications. The vulnerability scanning is checking known vulnerabilities for unpatched OS and running applications.

Using Kubernetes technology provides us with some features that distinct it from other type of deployments. These are the main features:

- **Service discovery and load balancing.**
- **Storage orchestration.**  Allows you to automatically mount a storage system.
- **Automated rollouts and rollbacks.**
- **Automatic bin packing.** You tell Kubernetes how much CPU and memory (RAM) each container needs.
- **Self-healing.** Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.
- **Secret and configuration management.** Kubernetes lets you store and manage sensitive information.
- Scale your application up and down

There are recommended configuration for each of the features to use by default when deploying MetaDefender Core in a Kubernetes cluster.

## Kubernetes Guide Structure

1. [Deployment Using Helm](https://www.opswat.com/docs/mdss/installation/deployment-using-helm)
2. [Replication & High Availability on K8S](https://www.opswat.com/docs/mdss/installation/replicas-on-k8s)
3. [Custom certificates on K8S](https://www.opswat.com/docs/mdss/installation/custom-certificates-on-k8s)
4. [OpenShift Considerations](https://www.opswat.com/docs/mdss/installation/openshift-considerations)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

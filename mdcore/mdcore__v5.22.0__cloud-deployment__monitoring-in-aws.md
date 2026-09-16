<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/cloud-deployment/monitoring-in-aws -->

# Monitoring in AWS

## [Health Check](/docs/mdcore/v5.22.0/cloud-deployment/monitoring-in-aws#health-check)

There are multiple factors that can result in failure of the system, some of them are AWS related (AZ fault, hardware fault) or application fault. Depending on the use case, each customer defines differently what application failed is.

Success

Starting with version 5.2.0, [Get health check status](/docs/mdcore/v5.22.0/metadefender-core#healthcheck) helps fetch the current health check status of the MetaDefender Core server.

### [Health Check for EC2 instance deployment](/docs/mdcore/v5.22.0/cloud-deployment/monitoring-in-aws#health-check-for-ec2-instance-deployment)

For generic hardware or AZ fault, we recommend deploying MetaDefender Core in a distributed environment as defined in [AMI - Distributed MetaDefender Deployment with Autoscaling](/docs/mdcore/v5.22.0/cloud-deployment/autoscaling-ec2-architecture). By deploying MetaDefender in different Availability Zones with a load balancer in front of them, you will always be sure that no hardware fault will result in service interruption.

### [Health Check for EKS deployment](/docs/mdcore/v5.22.0/cloud-deployment/monitoring-in-aws#health-check-for-eks-deployment)

Deploying MetaDefender Core in a Kubernetes cluster offer a high availability within the cluster thanks to the configured health check at the container level that use the "/readyz" endpoint and the auto-healing feature provide by Kubernetes

### [How to use the health check](/docs/mdcore/v5.22.0/cloud-deployment/monitoring-in-aws#how-to-use-the-health-check)

1. If you have an ELB in front of MetaDefender Core, configure it to do the health checks using the engines status.

   - How to setup ELB to do health checks: <https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-healthchecks.html>
   - For health check you should use the [GET Health Check API](https://docs.opswat.com/mdcore/metadefender-core#healthcheck)

     - If you've used [GET Engine Status](https://docs.opswat.com/mdcore/metadefender-core#enginesstatus), we'd recommend to move to the new dedicated Health Check API, since its validating the entire system's health, not just the engine's health.
2. In case you are not using an ELB or you would like to have a more advanced health check, our recommendation would be to setup a Lambda function to check on each MetaDefender instance. In case of the health check monitored via Lambda, you will have the flexibility to actually adapt based on the REST API response provided by MetaDefender. One of the following should apply:

   - If all engines are healthy, the instance is considered healthy
   - If some of the engines are not up to date or failing, based on the internal policy you might invalidate this MetaDefender instance.
   - If the REST API response is an error, the instance should be considered down
3. An even more advanced check can be considered actually submitting a file to be analyzed using a Lambda function. Note that depending on the file size and complexity, workflow configurations and the number of files in the queue, it might result in timing out the Lambda execution.

   - Submit always the same file to MetaDefender through the REST API
   - Compare the response with a baseline

### [Licensing](/docs/mdcore/v5.22.0/cloud-deployment/monitoring-in-aws#licensing)

To check the status of your MetaDefender Core license, please review the *Check Your License__Details* section on [License Activation](/docs/mdcore/v5.22.0/installation/metadefender-core-licensing) page. In case of monitoring the license information there is available an API endpoint to [get the license information](https://docs.opswat.com/mdcore/metadefender-core/ref#licenseget)

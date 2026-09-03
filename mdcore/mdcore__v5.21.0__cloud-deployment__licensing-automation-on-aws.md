<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/cloud-deployment/licensing-automation-on-aws -->

# Licensing Automation on AWS

To activate the instances where the MetaDefender products are running, it is needed to activate these products providing the LICENSE_KEY.

There are 2 options to manage the licensing that will automate the activation and deactivation of the products. This automation applies for the MetaDefender Core and MetaDefender ICAP Server products.

## [Setting Up Environment Variables](/docs/mdcore/v5.21.0/cloud-deployment/licensing-automation-on-aws#setting-up-environment-variables)

This option is the **default and recommended mechanism** to automate the licensing management, as this is the easiest way to activate and deactivate the products.

When passing the LICENSE_KEY as environment variables, to the user-data, it will set up the automation that will activate the product when the instance is started and will deactivate the product when the instance is terminated or stopped.

It is also recommended to indicate the APIKEY environment variable as this will set up the APIKEY to the admin user to be able to make requests to the MetaDefender Core API. In autoscaling deployment types it will help to manage all the instances with the same APIKEY when hitting the AWS Load Balancer.

### [Limitations](/docs/mdcore/v5.21.0/cloud-deployment/licensing-automation-on-aws#limitations)

#### [Deactivation with passwords other than instanceID](/docs/mdcore/v5.21.0/cloud-deployment/licensing-automation-on-aws#deactivation-with-passwords-other-than-instanceid)

In case the user changes the password to anything other than `instanceID`, the auto deactivation function of the shutdown script will fail. A way to fix this is to add `APIKEY` as a parameter.

#### [Windows images](/docs/mdcore/v5.21.0/cloud-deployment/licensing-automation-on-aws#windows-images)

Since the shutdown script on Windows platforms is configured using Local Group Policy, attaching Active Directory (AD) to a virtual machine (VM) created from our Windows images may cause the AD Group Policy to override the Local Group Policy, preventing the script from running.

## [Using Lambda Function](/docs/mdcore/v5.21.0/cloud-deployment/licensing-automation-on-aws#using-lambda-function)

Warning

Do not enable the Lambda function automation and set up the environment variables from the user data of the instances, as this will generate a conflict and neither option will work.

This option is for handling the license automation in case there are any issues when the logic, that is included inside the instances, fails.

This option can be enabled from the terraform project, see [How to deploy using Autoscaling EC2](/docs/mdcore/v5.21.0/cloud-deployment/autoscaling-ec2-deployment).

The automation consists of the following services:

- AWS Lambda function - to manage the activation/deactivation and store the deployment information.
- AWS Parameter Store - to store the deployment information
- Autoscaling Cloudwatch Events - Generated based on AWS ASG lifecycle hooks

## [Licensing when running in Kubernetes](/docs/mdcore/v5.21.0/cloud-deployment/licensing-automation-on-aws#licensing-when-running-in-kubernetes)

The licensing automation options when the MetaDefender products are installed in a Kubernetes cluster, are explained in [Licensing in K8S](/docs/mdcore/v5.21.0/container-deployment/licensing-in-k8s)

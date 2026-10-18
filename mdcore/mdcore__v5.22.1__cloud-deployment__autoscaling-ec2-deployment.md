<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/cloud-deployment/autoscaling-ec2-deployment -->

# Autoscaling EC2

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This is the guideline an autoscaling deployment of MetaDefender. In this example, besides the MetaDefender EC2 instance, additional resources are being generated and set up.

## [Prerequisites and Requirements](/docs/mdcore/v5.22.1/cloud-deployment/autoscaling-ec2-deployment#prerequisites-and-requirements)

**AWS knowledge**: This guide assumes familiarity with AWS services.

**AWS account**: needs permission to create AWS resources listed in [Autoscaling EC2](/docs/mdcore/v5.22.1/cloud-deployment/autoscaling-ec2-architecture)

**Tools to be used:** [Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)

### [System/OS requirements](/docs/mdcore/v5.22.1/cloud-deployment/autoscaling-ec2-deployment#systemos-requirements)

For OS, database type, 3rd party dependencies and storage requirements on Windows installations, please refer to the *Microsoft Windows Deployments* section of the [Recommended System Configuration](/docs/mdcore/v5.22.1/installation/recommended-system-configuration) page.

For OS, database type, 3rd party dependencies and storage requirements on Linux installations, please refer to the *Linux Deployments* section of the [Recommended System Configuration](/docs/mdcore/v5.22.1/installation/recommended-system-configuration) page.

## [Deploy using Terraform](/docs/mdcore/v5.22.1/cloud-deployment/autoscaling-ec2-deployment#deploy-using-terraform)

- Locally clone the [metadefender-csp](https://github.com/OPSWAT/metadefender-csp/tree/main/AWS) repository and go to AWS/autoscaling-group

BashCopygit clone git@github.com:OPSWAT/metadefender-csp.git
cd AWS/autoscaling-group

- Modify terraform.tfvars with the desired options

terraform.tfvarsCopy# General variables
MD_ENV_NAME = "metadefender"
MD_REGION = "eu-central-1"
#ACCESS_KEY_ID = "<ACCESS_KEY_ID>"
#SECRET_ACCESS_KEY = "<SECRET_ACCESS_KEY>"
MD_VPC_CIDR = "192.168.0.0/16"
PUBLIC_ENVIRONMENT = true
WARM_POOL_ENABLED = true
# MetaDefender Core variables
DEPLOY_CORE = "false"
CORE_PRODUCT_ID = "ani6v4vb5z4t87cymrfg3m451" # For Windows it is "9s8powksm1cj7fuafdnv0sfj9"
CORE_INSTANCE_TYPE = "c5.2xlarge"
LICENSE_KEY_CORE = ""
CORE_PWD = "admin"
CORE_PORT = 8008

- Run terraform apply and check the resource to be create, after that enter "y"

BashCopyterraform apply

<!-- source: https://www.opswat.com/docs/supply-chain/integrations/add-an-amazon-ecr-service -->

# Add An Amazon ECR Service

In order to integrate Amazon ECR with MetaDefender Software Supply Chain, please follow these steps:

![](https://uploads.developerhub.io/prod/jdK6/xa4442fs7qxk7wyvzvapsdhts0jajsocnji69efch8kdpbvw9qx1u84yntniddpe.png)

1. From the left side menu, navigate to **Inventory** and choose **Amazon ECR**
2. Give your connection a name so you can easily identify it later.
3. Enter your **AWS Access Key ID**. Scroll to the end of this page for more details.
4. Enter your **AWS Secret Access Key**. Scroll to the end of this page for more details.
5. Select your **AWS Region** where your repositories are located.
6. Select **Add Connection** in order to finish the process.

### Where can I find the Access Key ID and Secret Access Key?

To generate an Access Key ID / Secret Access Key pair please follow these steps:

1. Log in to [IAM Console](https://console.aws.amazon.com/iam/home?region=us-east-1#home) and go to **Users**.
2. In the **Details** pane, click on the appropriate IAM user or create one if none exists.
3. From the **Security Credentials** tab, click **Create Access Key**.

> **Info**
>
> If you already have a maximum of two access keys - active or inactive - you must delete one first before proceeding. If you need more than two root access keys, IAM users (each of whom can be assigned their own access keys) would probably better suit your requirements.

### Necessary AWS policies

- `"ecr:BatchGetImage"`
- `"ecr:BatchCheckLayerAvailability"`
- `"ecr:CompleteLayerUpload"`
- `"ecr:DescribeRegistry"`
- `"ecr:DescribeRepositories"`
- `"ecr:GetRegistryPolicy"`
- `"ecr:GetDownloadUrlForLayer"`
- `"ecr:GetAuthorizationToken"`
- `"ecr:ListTagsForResource"`
- `"ecr:ListImages"`
- `"ecr-public:DescribeRepositories"`

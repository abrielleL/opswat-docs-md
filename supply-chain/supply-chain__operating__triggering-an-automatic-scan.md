<!-- source: https://www.opswat.com/docs/supply-chain/operating/triggering-an-automatic-scan -->

# Event based scanning

Event based scanning automatically triggers a scan whenever something changes in your repository - a push, a merge request, or an artifact event.

Most integrations trigger scans by connecting your service provider to MetaDefender Software Supply Chain through a native webhook. Amazon ECR is the exception: it is triggered through an external AWS EventBridge + Lambda integration (not a native MetaDefender Software Supply Chain webhook subscription).

## Setup Steps

- Create a custom workflow on the **Workflows** page. The built-in Default Workflow cannot be used for webhooks.
- Go to **Inventory**, select the service connection, and click **Start Job**:

![](https://uploads.developerhub.io/prod/jdK6/19mqrrao6pbctjxytm0q7gp1awaogy1td5uqtw6psoy9fov4lt720mkyi6u8oghz.png)

- In the New Job panel, select the repository you want to monitor and choose your custom workflow:

![](https://uploads.developerhub.io/prod/jdK6/ptdg7r4e1nb6hvxc9hcltfy4ovc430uvuacllou19iv2q76k5r4tg3daj0e9eokz.png)

- Switch to the **Real-Time Scan** tab. Once a custom workflow is selected, the **Webhook URL** is generated - copy it using the button next to the field:

![](https://uploads.developerhub.io/prod/jdK6/dl4xeuu2pdjgdevhcqnvibi0xfwiqvwp8ozkpsbltxmqlxiszu5kys9isrfya4ad.png)

- Configure the webhook in your service provider using the copied URL (see the provider examples below), then click **Create**.

## Examples

Step-by-step examples for each provider can be found in the Event based scanning section:

- [Bitbucket Cloud](https://www.opswat.com/docs/supply-chain/operating/bitbucket-cloud)
- [Bitbucket Data Center](https://www.opswat.com/docs/supply-chain/operating/bitbucket-data-center)
- [GitHub](https://www.opswat.com/docs/supply-chain/operating/github)
- [GitLab](https://www.opswat.com/docs/supply-chain/operating/gitlab)
- [JFrog Binary](https://www.opswat.com/docs/supply-chain/operating/jfrog-binary)
- [Harbor](https://www.opswat.com/docs/supply-chain/operating/harbor)
- [Nexus Repository](https://www.opswat.com/docs/supply-chain/operating/nexus-repository)
- [AWS ECR](https://www.opswat.com/docs/supply-chain/operating/aws-ecr)

The example pages contain provider-side instructions which are subject to change in case the service providers change their user interface.

## Supported Events

Currently, webhooks are supported for:

- **Bitbucket Cloud** - Repository: Push; Pull request: Opened, Merged
- **Bitbucket Data Center** - Repository: Push; Pull request: Opened, Merged
- **GitHub and GitHub Enterprise** - Repository: Push; Pull request: Opened, Merged
- **GitLab** - Push; Merge Request
- **JFrog Binary** - Artifact was cached, copied, created, or moved
- **JFrog Container** - Docker tag pushed
- **Harbor** - Artifact pushed
- **Nexus Binary** - Component created or updated
- **Amazon ECR** - Image push (via AWS EventBridge: ECR Image Action / PUSH / SUCCESS). This uses an EventBridge + Lambda integration rather than a webhook subscription.

## How it works

- Every time a **merge request** is opened or merged on the monitored repository, a scan is triggered on the **source branch** of the merge request, not on the target branch.
- Every time a **push** is made to the monitored repository, a scan is triggered on the **default branch** of the repository.
- For **Amazon ECR**, an image push event triggers a scan of the exact pushed image tag.
- For **JFrog Binary**, every time a configured artifact event happens (an artifact was cached, copied, created, or moved in the selected repository), a scan of that repository is triggered.
- For **JFrog Container** and **Harbor**, an image push triggers a scan of the pushed image tag. If a Harbor image has no tag, MDSSC scans it by its digest.
- For **Nexus Binary**, a created or updated component triggers a scan of that component version, not the whole repository.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)

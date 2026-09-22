<!-- source: https://www.opswat.com/docs/supply-chain/operating/triggering-an-automatic-scan -->

# Event based scanning

Event based scanning automatically triggers a scan whenever something changes in your repository - a push, a merge request, or an artifact event.

Most integrations trigger scans by connecting your service provider to MetaDefender Software Supply Chain through a native webhook. Amazon ECR is the exception: it is triggered through an external AWS EventBridge + Lambda integration (not a native MetaDefender Software Supply Chain webhook subscription).

## Setup Steps

- Create a custom workflow on the **Workflows** page. The built-in Default Workflow cannot be used for webhooks.
- Go to **Inventory**, select the service connection (should be a supported service)
- Find the repository you want to monitor and click on the 🔗 icon:

![](https://uploads.developerhub.io/prod/jdK6/6zzydvqmkoc5mskqlsqfwzj46pkiuc39zii29eymtq85rwn58ic63ku98wzr8ubt.png)

- The following drawer is now visible, from here you need to choose your custom workflow:

![](https://uploads.developerhub.io/prod/jdK6/0wqztcd36ekyfp8v5htjxhnqoplk52exjbhburtns02anqlshjtpphyqrllv5k1f.png)

- Once a custom workflow is selected, the **Webhook URL** is generated - copy it using the button next to the field:

![](https://uploads.developerhub.io/prod/jdK6/ffa72ndp3q562tse3ocyephdehvin251yqq4xs7j9sa6kmw1x28wsrmjp1i50pu9.png)

- Configure the webhook in your service provider using the copied URL (see the provider examples below) and then based on your webhook configuration a scan will be triggered.

## Examples

Step-by-step examples for each provider can be found in the Event based scanning section:

- [Bitbucket Cloud](https://www.opswat.com/docs/supply-chain/operating/bitbucket-cloud)
- [Bitbucket Data Center](https://www.opswat.com/docs/supply-chain/operating/bitbucket-data-center)
- [GitHub](https://www.opswat.com/docs/supply-chain/operating/github)
- [GitLab](https://www.opswat.com/docs/supply-chain/operating/gitlab)
- [JFrog Binary](https://www.opswat.com/docs/supply-chain/operating/jfrog-binary#how-to-configure-real-time-processing-for-jfrog-binary)
- [AWS ECR](https://www.opswat.com/docs/supply-chain/operating/aws-ecr)

The example pages contain provider-side instructions which are subject to change in case the service providers change their user interface.

## Real Time Processing (RTP)

Real Time Processing (RTP) is currently available only for **JFrog Binary** service connections. To set it up, see [JFrog page](https://www.opswat.com/docs/supply-chain/operating/jfrog-binary).

## Supported Events

Currently, webhooks are supported for:

- **Bitbucket Cloud** - Repository: Push; Pull request: Opened, Merged
- **Bitbucket Data Center** - Repository: Push; Pull request: Opened, Merged
- **GitHub** - Repository: Push; Pull request: Opened, Merged
- **GitLab** - Push; Merge Request
- **JFrog Binary** - Artifact was cached, copied, created, or moved
- **Amazon ECR** - Image push (via AWS EventBridge: ECR Image Action / PUSH / SUCCESS). This uses an EventBridge + Lambda integration rather than a webhook subscription.

## How it works

- Every time a **merge request** is opened or merged on the monitored repository, a scan is triggered on the **source branch** of the merge request, not on the target branch.
- Every time a **push** is made to the monitored repository, a scan is triggered on the **default branch** of the repository.
- For **Amazon ECR**, an image push event triggers a scan of the exact pushed image tag.
- For **JFrog Binary**, every time a configured artifact event happens (an artifact was cached, copied, created, or moved in the selected repository), a scan of that repository is triggered.

##

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)

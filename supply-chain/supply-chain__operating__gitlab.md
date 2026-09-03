<!-- source: https://www.opswat.com/docs/supply-chain/operating/gitlab -->

# GitLab

1. Go to your **GitLab** instance → select the repository chosen in **MetaDefender Software Supply Chain** → Settings → Webhooks → Add new webhook

![](https://uploads.developerhub.io/prod/jdK6/r54vvn8rdsugxgy1mpv3hmhkdmfagw8qnr2t5zbhgsaag3qb4bnc0yhu7ptsulxf.png)

2. Fill the necessary details by giving a name (optional), the **URL** will be the generated URL from **MetaDefender Software Supply Chain**, select a compatible **event type** (in this example, we use push event) and also add a custom header including the API Key:

![](https://uploads.developerhub.io/prod/jdK6/w8tqehv0v2v5hrhmve7ee5sn35d6u2aa17bankxpvee0bh82uzluzvv86r6fbbuk.png)

3. After that hit the `Add webhook`  button and the new webhook will be added to the list:

![](https://uploads.developerhub.io/prod/jdK6/a41f4r1rny7whsfa19uvwjiq2q9yd7gwr7doptcejs8fiamkvov4tv8t6kt9kwex.png)

Now, when something is pushed into the GitLab repository, a scan will be automatically triggered.

<!-- source: https://www.opswat.com/docs/supply-chain/operating/nexus-repository -->

# Nexus Repository

Event-based scanning is available for Nexus Binary connections. It is not available for Nexus Container connections.

1. Log in to Nexus Repository as an administrator.
2. Click the gear icon to open the administration menu, then select "System" → "Capabilities":

![](https://uploads.developerhub.io/prod/jdK6/buo5ai0aoc5uu7dpu4d74m7zg93w79w2z6uo4e40izv8r4yqh8jx5bchboapxjvz.png)

3. Click "Create capability" and select "Webhook: Repository". The webhook configuration page opens:

![](https://uploads.developerhub.io/prod/jdK6/c9ye8tz8knyefb4z9p4rppnbgyuy4jdurshiuubz3mrooz71av6gli7kqftikqmc.png)

- Under "Repository", select the repository that needs event-based scanning.
- Under "Event Types", select "component".
- Insert the MDSSC Webhook URL that you generated for this connection into the "URL" field.
- Insert your MDSSC API key into the "Secret Key" field.

> **Attention:**
>
> Use the API key of the user who generated the Webhook URL. If this user generates a new API key, update the Secret Key in Nexus.

4. Click "Create capability".
5. To test the webhook, upload a component to the repository. MDSSC scans the uploaded component version, not the whole repository.

> **Info**
>
> MDSSC scans components that are created or updated. Deleted components, asset events, and Docker and Helm components do not start a scan. Nexus does not have a test button, so upload a component to test the webhook.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)

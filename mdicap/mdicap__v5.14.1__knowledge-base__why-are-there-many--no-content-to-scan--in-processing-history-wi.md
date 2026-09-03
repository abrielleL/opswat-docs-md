<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/knowledge-base/why-are-there-many--no-content-to-scan--in-processing-history-wi -->

# Why are there many "No content to scan" in Processing History with ICAP and F5 integration?

This article applies to all MetaDefender ICAP Server releases deployed on Windows and Linux systems when integrated with **F5**.

## [Issue](/docs/mdicap/v5.14.1/knowledge-base/why-are-there-many--no-content-to-scan--in-processing-history-wi#issue)

In **MetaDefender ICAP UI** > **History** > **Processing History,** you may notice many entries labeled “No Content to Scan”.

## [Root cause](/docs/mdicap/v5.14.1/knowledge-base/why-are-there-many--no-content-to-scan--in-processing-history-wi#root-cause)

F5 is sending multiple **HTTP GET requests** to MetaDefender ICAP server.

- These requests do not include any body content.
- Since there is no payload to inspect, the MetaDefender ICAP server records the events as “No content to scan”.

## [Solution](/docs/mdicap/v5.14.1/knowledge-base/why-are-there-many--no-content-to-scan--in-processing-history-wi#solution)

To reduce unneccessary scan requests, configure F5 to only send requests that includes content (e.g, POST requests).

1. Create a Policy Create a **Policy1** with two rules **to filter and only scan POST request**

- Rule 1

- Rule 2

2. Publish the policy

3. Attach the Policy to the virtual server

- Edit your **WebApp** virtual server

- Navigate to **Resources** tab, under **iRules**, click **Manage** button

- Enable Policy1 (created in Step 1)

For detailed F5 configuration guidelines,see: [4.5. Managing ICAP Policies](https://clouddocs.f5.com/sslo-deployment-guide/sslo-08/chapter4/page4.5.html)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

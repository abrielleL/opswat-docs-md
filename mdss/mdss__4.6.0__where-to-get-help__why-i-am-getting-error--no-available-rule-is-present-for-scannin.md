<!-- source: https://www.opswat.com/docs/mdss/4.6.0/where-to-get-help/why-i-am-getting-error--no-available-rule-is-present-for-scannin -->

# Why I am getting error "No available rule is present for scanning"

When triggering a scan, you may encounter a scan failure with the following error message:

> **Error**
>
> opswat.mdcs.scanning.ScanFailedException: InitiateScanCommandHandler: Scan request for object failed. StatusCode: InternalServerError Error: No available rule is present for scanning.

![](https://uploads.developerhub.io/prod/k8zL/uuo3gtvxocg581tu0xngai99o819wl71ythvf94ig93ub6lozua52b4hgk362ja2.png)

## Cause

This error typically occurs when the workflow name configured in MetaDefender for Secure Storage (MDSS) does not match the workflow name set in MetaDefender Core.

MetaDefender Storage Security

![](https://uploads.developerhub.io/prod/k8zL/w9lcwwbxzaefiiw0p6qny2m2e7hw2ab4qnrhx5z26v9tgraj6y3ikpoaj5jjuw01.png)

MetaDefender Core

![](https://uploads.developerhub.io/prod/k8zL/vvc8q6hebrqedw5cxdlmtap7c3onclzrcvq92i6dm36dbsydqx3uptoal4q5hqda.png)

## Steps to Resolve:

1. **Log into MetaDefender Core**
   - Navigate to Workflows.
   - Identify the workflow associated with MDSS.
   - The workflow name should be either: "MetaDefender Storage Security" or "MetaDefender for Secure Storage"
2. **Verify and Update the Workflow in MDSS**
   - If the workflow name in Core is "MetaDefender Storage Security", log into MDSS Configuration.
   - Go to **Workflows** and click on your workflow

![](https://uploads.developerhub.io/prod/k8zL/zxs4y0rlqd7gt9qpwul1py6sk50im7b8s4k70890tjtnxnbt8ud736yd0jacve0a.png)

- Edit the scan configuration and update the rule name to "MetaDefender Storage Security".

![](https://uploads.developerhub.io/prod/k8zL/ao10stegttdciglx6ldqy3lirnc8laxqrhcoevzsp9oaqay8f7ldiptw6ekvxb3l.png)

- Ensure the workflow name exactly matches the one in Core.

3. **Apply Changes and Restart the Service**

- Click “Save” to save the configuration.
- Restart the scanning service if necessary and retry the scan to verify if the issue is resolved.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

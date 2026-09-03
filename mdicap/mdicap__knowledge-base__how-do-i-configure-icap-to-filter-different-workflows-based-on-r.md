<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/how-do-i-configure-icap-to-filter-different-workflows-based-on-r -->

# How do I configure ICAP to filter different workflows based on request headers?

MetaDefender ICAP supports workflow filtering based on request headers. It is possible to fine-tune ICAP’s workflow, by **configuring the proxy to add request headers** and **utilize ICAP’s** **[request filter](/docs/mdicap/operating/security-rules-policy#request-filter) **for those added headers.

Use Case:

In practice, you can **customize the request headers inserted by the proxy**, and the **corresponding request filter in ICAP’s workflow settings**, depending on your specific use case.

Take the below example, the proxy is configured to insert an additional header (based on file size), and MetaDefender ICAP is configured to filter different workflows (based on the value of the inserted header):

- Default workflow for all data → Default workflow in MD Core
- Header for small files → Workflow dedicated to handle small files in MD Core
- Header for big files → Workflow dedicated to handle big files in MD Core

## [Example](/docs/mdicap/knowledge-base/how-do-i-configure-icap-to-filter-different-workflows-based-on-r#example)

It is possible to configure the proxy and ICAP’s request filter following the outline below:

1. In ICAP, create 3 workflows:

   1. Small → The server profile has a Core with small files workflow.
   2. Large →The server profile has a Core with big files workflow.
   3. Default

In each workflow, you can add the **HTTP Header** filter corresponding workflow name

2. For example: using a custom header “ICAPWorkflow” with values “small” and “large” (but you can use any header as needed).

3. When the request has the **“ICAPWorkflow” HTTP header** (you can use the backend server, reverse proxy server, or anything else to insert it) with the value:

   1. “small” → Will be processed by ICAP server’s small workflow → Send to MD Core small workflow.
   2. “large” → Will be processed by ICAP server’s large workflow → Send to MD Core large workflow.

Support:

For further assistance regarding **Configure MetaDefender ICAP to use different workflows based on file size**, please [**create a support case or chat with our support engineer**](https://my.opswat.com/portal/support).

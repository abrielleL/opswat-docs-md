<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/what-is-the-expected-metadefender-storage-security-remediation-b -->

# What is the expected MetaDefender Storage Security Remediation Behavior Behind F5 Load Balance?

> **Check Your Version:**
>
> This article applies to all MetaDefender Storage Security versions.

## Issue:

When F5 is configured with cookie-based persistence, MetaDefender Storage Security remediation could fail. This could occur if the XML provided was not well-formed or was not valid during initial communication. **cookie-based persistence on F5** causes inconsistent routing of related S3 API requests during remediation workflows.

## Description

When persistence is enabled, the F5 load balancer modifies the headers cookies of API requests from  MetaDefender Storage Security to the S3 compatible storage, causing API responses to get corrupted and not being processed by our MetaDefender Storage Security.  While switching F5 to source address persistence seems the least invasive there is no guarantee that it will not modify the headers for tracking.

## Mitigation:

1. Disable persistence for the virtual server handling S3 traffic, OR
2. Create a separate virtual server with FastL4 profile for S3 connections

> **Info:**
>
> S3 API calls are stateless and don't require session affinity - persistence only adds processing overhead that corrupts the XML payloads.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

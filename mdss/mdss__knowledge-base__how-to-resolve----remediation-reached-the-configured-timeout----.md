<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/how-to-resolve----remediation-reached-the-configured-timeout---- -->

# How to resolve “Remediation Reached the Configured Timeout” for SMB Storage?

**Check Your Version:** This article applies to all MetaDefender Storage Security

## [**Issue**](/docs/mdss/knowledge-base/how-to-resolve----remediation-reached-the-configured-timeout----#issue)

When running a **Discovery workflow with Remediation** against SMB storage, some files may fail with the following error:

> opswat.mdcs.job.dispatcher.ObjectProcessingStuckException: Remediation reached the configured timeout ---> System.TimeoutException: 1 or more hours passed since MetaDefender Storage Security started remediations for the file --- End of inner exception stack trace ---

## [**Possible issues**](/docs/mdss/knowledge-base/how-to-resolve----remediation-reached-the-configured-timeout----#possible-issues)

By default, MetaDefender Storage Security waits up to **1 hour** for a remediation task to complete. If the remediation process takes longer than the configured timeout, the file is marked as failed.

This can happen when:

- The server does not meet the recommended system requirements.
- The SMB storage configuration is not optimized for MetaDefender Storage Security.
- The storage contains a large number of files or large file sizes.
- SMB remediation takes longer than NFS remediation due to protocol or environment differences.

## [**Resolutions**](/docs/mdss/knowledge-base/how-to-resolve----remediation-reached-the-configured-timeout----#resolutions)

### [**1. Verify the Server Meets System Requirements**](/docs/mdss/knowledge-base/how-to-resolve----remediation-reached-the-configured-timeout----#1-verify-the-server-meets-system-requirements)

Confirm that the server hosting MetaDefender Storage Security meets the required system specifications.

Refer to the official system requirements:

[General System Requirements - MetaDefender Storage Security](https://www.opswat.com/docs/mdss/getting-started/general-system-requirements)

### [**2. Use the Recommended SMB Storage Approach**](/docs/mdss/knowledge-base/how-to-resolve----remediation-reached-the-configured-timeout----#2-use-the-recommended-smb-storage-approach)

For SMB-compatible storage, OPSWAT highly recommends using the recommended integration approach documented below:

[Recommended approach when adding SMB units on Linux deployments - MetaDefender Storage Security](https://www.opswat.com/docs/mdss/integrations/recommended-approach-when-adding-smb-compatible-storage)

This approach can help improve reliability and reduce remediation-related timeout issues when working with SMB shares.

### [**3. Increase the Remediation Timeout**](/docs/mdss/knowledge-base/how-to-resolve----remediation-reached-the-configured-timeout----#3-increase-the-remediation-timeout)

If remediation tasks require more than the default timeout of **1 hour**, increase the configured remediation timeout (to 3 hours for example).

On the MetaDefender Storage Security server, edit the `customer.env` file and add the following value:

REMEDIATION_STUCK_TIMEOUT_HOURS=3

If this value already exists, update it to:

REMEDIATION_STUCK_TIMEOUT_HOURS=3

For instructions on modifying `customer.env`, refer to:

[Custom configuration - MetaDefender Storage Security](https://www.opswat.com/docs/mdss/configuration/custom-configuration)

**Support:** If **Further Assistance** is required, please collect a new MetaDefender Storage Security support package and proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

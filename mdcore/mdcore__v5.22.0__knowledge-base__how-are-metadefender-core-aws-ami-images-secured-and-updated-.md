<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-are-metadefender-core-aws-ami-images-secured-and-updated- -->

# How are MetaDefender Core AWS AMI images secured and updated?

## [Patching & Security Updates:](/docs/mdcore/v5.22.0/knowledge-base/how-are-metadefender-core-aws-ami-images-secured-and-updated-#patching--security-updates)

1. How quickly are critical security patches applied to the AMI?

`For vulnerabilities detected from the MDCore application level, they will be patched in the next release of MD Core version. For vulnerabilities detected from the OS level, they will be patched and re-published within AWS policy.`

2. Is the AMI hardened for secure configuration?

`Yes. If the AMIs don’t match the security policy from AWS, they won’t let us release them to the marketplace`

3. Is there a predefined SLA for security fixes?

`We follow the SLA from AWS. If we don’t fix the issue within the AWS SLA, they will remove our AMIs from the marketplace`

## [AMI Lifecycle & Versioning:](/docs/mdcore/v5.22.0/knowledge-base/how-are-metadefender-core-aws-ami-images-secured-and-updated-#ami-lifecycle--versioning)

How frequently is a new AMI released?

It will be released with every version of MD Core. After MetaDefender Core new version is released on [My OPSWAT](https://my.opswat.com/home/metadefender-core) , it takes us approximately 1 week after public release to publish on AMI.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).

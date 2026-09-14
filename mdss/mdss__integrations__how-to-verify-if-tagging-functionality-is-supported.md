<!-- source: https://www.opswat.com/docs/mdss/integrations/how-to-verify-if-tagging-functionality-is-supported -->

# How to verify if tagging functionality is supported?

Object tagging functionality is supported for AWS S3 and other S3-compatible storage providers. This document explains the permission requirements and troubleshooting steps for tagging functionality.

MDSS verifies the following permissions during storage integration or modification:

jsonCopy"s3:GetObject",
"s3:PutObject",
"s3:DeleteObject"
"s3:PutObjectTagging",
"s3:GetObjectTagging",
## [Status Conditions](/docs/mdss/integrations/how-to-verify-if-tagging-functionality-is-supported#status-conditions)

### [Disabled Tagging Functionality](/docs/mdss/integrations/how-to-verify-if-tagging-functionality-is-supported#disabled-tagging-functionality)

Tagging functionality may be unavailable due to:

1. Missing core permissions (`s3:GetObject`, `s3:PutObject`, `s3:DeleteObject`)

   - When these are missing, tagging functionality cannot be tested and will be disabled
2. Missing tagging permissions (`s3:PutObjectTagging`, `s3:GetObjectTagging`)

   - When these are missing, tagging functionality will not be supported
3. Storage provider limitations

   - If the S3-compatible storage does not support object tagging

## [Verification Process](/docs/mdss/integrations/how-to-verify-if-tagging-functionality-is-supported#verification-process)

Permission verification occurs:

- When storage is first integrated with MDSS
- When storage configuration is edited

## [Troubleshooting](/docs/mdss/integrations/how-to-verify-if-tagging-functionality-is-supported#troubleshooting)

If tagging functionality is disabled but required permissions have been added:

1. Edit the storage configuration in MDSS
2. Save changes without modifying any settings

This action will trigger a re-verification of permissions and enable tagging functionality if all requirements are met.

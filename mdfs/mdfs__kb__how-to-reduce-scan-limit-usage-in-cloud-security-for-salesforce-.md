<!-- source: https://www.opswat.com/docs/mdfs/kb/how-to-reduce-scan-limit-usage-in-cloud-security-for-salesforce- -->

# How to reduce Scan Limit Usage in MetaDefender for Salesforce?

#### [Issue](/docs/mdfs/kb/how-to-reduce-scan-limit-usage-in-cloud-security-for-salesforce-#issue)

While using MetaDefender for Salesforce, you may want to reduce the number of scans performed.

#### [Cause](/docs/mdfs/kb/how-to-reduce-scan-limit-usage-in-cloud-security-for-salesforce-#cause)

If not optimized, uploading the same file multiple times will cause the system to rescan it each time, unnecessarily consuming your scan quota.

#### [Solution](/docs/mdfs/kb/how-to-reduce-scan-limit-usage-in-cloud-security-for-salesforce-#solution)

To improve efficiency and reduce scan volume, we recommend enabling the Reuse Old Scan Results feature, available starting in version 5.4 of MetaDefender for Salesforce. This feature allows the system to skip scanning files that have already been scanned within a specified time interval. This feature applies when files are uploaded. If a file was previously scanned within the configured threshold, it will not be processed again, reducing overall scan volume.

#### [Benefits](/docs/mdfs/kb/how-to-reduce-scan-limit-usage-in-cloud-security-for-salesforce-#benefits)

- Prevents duplicate scan of the same uploaded file.
- Improves system efficiency and performance.
- Reduces unnecessary consumption of your scan limit.

To enable this feature, please navigate to OPSWAT Settings -> Scan rules -> add a value for the number of days a scan result should be valid in the reuse scan results section and then click on save as per the below screenshot:to-generated with new documentation

Once enabled, the application will automatically reuse scan results for any uploaded file already processed within the configured interval.

This feature is available starting with MetaDefender for Salesforce v5.4. Please ensure the product is updated to use this capability.

Support:

If you encounter any issues during the activation process or require further assistance, please contact OPSWAT support via My OPSWAT at: <https://my.opswat.com/portal/home>

Our support team will be able to provide you with the necessary guidance and resolution for any license-related concerns.

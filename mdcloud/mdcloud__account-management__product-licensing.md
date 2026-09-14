<!-- source: https://www.opswat.com/docs/mdcloud/account-management/product-licensing -->

# Product Licensing

**MetaDefender Cloud** comes in three different flavors: **Standard**, **Professional**, and **Enterprise**.

- The **Standard** tier is geared towards personal users and very small startups that do not have a high volume of files to scan.
- The **Professional** tier offers a general-purpose license tailored for most small to mid-sized organizations.
- The **Enterprise** tier is designed for large organizations in search of a robust cybersecurity solution and the highest scan time and availability SLAs.

All the information regarding our Product Licensing can be found here: <https://metadefender.opswat.com/licensing>

Every license tier features a distinct configuration tailored to meet the specific requirements of your business.

**Number of engines** - represents the AV engines used to scan a file for each license tier.

**File size limit** - represents the maximum file size supported for each license tier.

Info

For requests > 1GB requests will need to include a signed URL of the file instead of the actual file itself.

**Throttling (req/min)** - represents the number of the requests a user can submit per minute. Applies to file uploads and bulk requests. It is implemented to prevent excessive usage, abuse, or overloading of a system or service, ensuring fair and efficient resource allocation. Exceeding this limit may result in errors, or temporary suspension of access.

**Prevention limit** - You have the option to choose between 'Daily' and 'Monthly,' providing you with flexibility in organizing and managing the usage limits based on your preferences.

**Max files in archive** - The maximum allowable number of files that can be included in an archive.

**Archive recursion level** - refers to the maximum depth of an archive, and this value varies for each product flavor.

**Request priority (queue)** - Depending on the tier, files are retrieved from specific waiting queues. Standard tier utilizes the Low queue, Professional tier utilizes the Medium queue, and Enterprise tier utilizes the High queue.

**Availability SLA** - Our Cloud product ensures service reliability with an Availability SLA. Starting at 99.5% for the Standard tier, it goes up to 99.9% for the Enterprise tier, providing users with consistent and dependable accessibility.

**Scan time SLA** - Our response time metrics exclude archive file processing, recursive file analysis involving multiple files (even when a single file is submitted), and dynamic analysis. In these metrics, P50 denotes the median value of all requests in a given month, while P90 represents the 90th percentile of all requests during that month.

**RTO -** Our sets the maximum time for restoring a system or process after a disruption to prevent adverse consequences. RTO varies across tiers, ranging from 24 hours for Standard to 4 hours for Enterprise customers.

**RPO** - The maximum acceptable data loss, indicating the point in time to which data must be recovered after an incident. RTO varies across tiers, ranging from 24 hours for Standard to 4 hours for Enterprise customers.

**Monthly rate limits** - only the Enterprise customers can opt in between 'Daily' and 'Monthly,' providing you with flexibility in organizing and managing the usage limits based on your preferences.

**Ability to exceed limit** - We provide users with the option to surpass the rate limit, specifying the extent to which a user can exceed the limit before the API initiates request blocking.

**Deep CDR** - Please note, MetaDefender Cloud is licensed by number of API calls. If you wish to do multiscanning and CDR on every file uploaded that will count as 2 calls per file. Therefore you will need to purchase a daily API call limit twice that of your daily file traffic.

**Private Scanning** - For all its standard, professional and enterprise users, MetaDefender Cloud provides the ability to scan files privately. This **private scanning** feature is available through the MetaDefender Cloud APIs, metadefender.opswat.com website and the MetaDefender Chrome Extension. All files scanned in private mode are not stored or shared, although scan results will remain available in the MetaDefender Cloud database.

**Private Processing** - To provide our customers with an additional level of privacy, we offer **private processing** in addition to private scanning. When `privateProcessing`is set to 1, this feature will not only immediately remove files after analysis is done, but also ensure that the results of those scans will only be available to the owner who submitted the files for scanning in the first place (only with the same API Key).

**End to End Encryption** - Secure private resources by employing customer-provided public keys to encrypt sanitized versions of files.

**Organizations** - This feature is offered to Professional and Enterprise customers, allowing them to create multiple Organizations. It helps group users with RBAC, assigns administrators for organization management, and facilitates license management. Each organization has Admins with full rights and Users who can view licenses. Users can be added via invitation emails from the organization UI. Check the [Sub-Organization](https://docs.opswat.com/mdcloud/account-management/sub-organizations) page for more details.

**Reporting** - We provide with custom made reports created based on the monthly usage and can be provided on demand.

**Notifications/Alerts** - We provide you with the option to receive continuous updates whenever a new user is added to the organization, removed from it, or when there is a change in a user's role. Additionally, you can stay informed about other noteworthy information. Furthermore, we offer notifications for tracking the percentage of your daily limit reached for both the Prevention API and Reputation API. These alerts can be delivered directly within the application or sent to you via email, according to your preference.

**IP Range Restrictions** - On the Security page of your account, you have the capability to specify IP ranges for whitelisting.

**mTLS** - Enterprise clients can establish a secure connection to our API through Mutual TLS (mTLS), an extension of the TLS protocol. With mTLS, both parties are required to authenticate each other, reinforcing the security of communication for enhanced trust and protection.

**Customer Provided IDP** - We offer you the opportunity to "Bring Your Own Identity Provider" helping you to integrate your preferred authentication methods, enhancing flexibility, security, and user experience in accessing MetaDefender Cloud.

**Custom Domain** - We offer you the opportunity to create your own distinct domain for a more distinctive and memorable online presence within MetaDefender Cloud.

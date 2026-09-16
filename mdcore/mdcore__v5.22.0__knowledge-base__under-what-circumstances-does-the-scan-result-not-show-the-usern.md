<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/under-what-circumstances-does-the-scan-result-not-show-the-usern -->

# Under what circumstances does the scan result not show the username?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

When MetaDefender Core scans the files from each session, each session represents the information on the user that scans the files.

Scan History exported from csv

There are 2 ways to scan without username

## [1. Scanning Without Logging In](/docs/mdcore/v5.22.0/knowledge-base/under-what-circumstances-does-the-scan-result-not-show-the-usern#1-scanning-without-logging-in)

As shown in the image above, **MetaDefender Core allows file scanning without requiring user authentication**. When a file is scanned without logging in:

- No username or user-specific details are stored in the scan record.
- The file can still be processed and analyzed, but there is no user identification in the logs.
- This applies to scans initiated via the **public web interface** where authentication is not required.

## [2. Scanning Files Through the REST API](/docs/mdcore/v5.22.0/knowledge-base/under-what-circumstances-does-the-scan-result-not-show-the-usern#2-scanning-files-through-the-rest-api)

When scanning files through the **MetaDefender Core REST API**, the behavior differs:

- The scan session is tracked by the API authentication token or session key.
- If an authenticated API request is used, the scan can be tied to the system or user executing the request.
- If performed anonymously (without authentication), the scan will not contain identifiable user details, similar to the public web interface.

## [3. After a User has been Deleted](/docs/mdcore/v5.22.0/knowledge-base/under-what-circumstances-does-the-scan-result-not-show-the-usern#3-after-a-user-has-been-deleted)

If a certain user has been deleted after performing multiple scans, that user won’t appear in the Processing History page anymore.

- This also applies if the scan request has been made through the REST API using the deleted user’s credentials in order to obtain a session ID.

## [Recommendations](/docs/mdcore/v5.22.0/knowledge-base/under-what-circumstances-does-the-scan-result-not-show-the-usern#recommendations)

**Export reports before deleting users** If user accounts must be removed, export Scan History beforehand to preserve user attribution.

**Restrict WebScan workflows to authenticated users** Set workflow access to **Restrict access to the following roles: Every authenticated** to prevent anonymous scans.

**Use separate API credentials** For REST API integrations, use different API keys for each application or service to improve scan traceability.

**Track user attribution externally** If scans are initiated through applications, pass end-user identifiers through metadata or custom headers and correlate them using external logging systems such as SIEM platforms.

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).

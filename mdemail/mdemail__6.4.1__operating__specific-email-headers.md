<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/operating/specific-email-headers -->

# Specific email headers

The following email headers are added once the email is processed by MetaDefender Email Gateway Security. These headers can be used for example for custom rules on mail servers such as spam rules using X-Metadefender-Core-Result.

Syntax

In header keys only a specific set of characters are allowed. Custom headers (see [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy)) are validated for allowed characters.

In header values only a specific set of characters are allowed. If a forbidden character is provided (for example *:* (colon, which is the separator between the header key and value)), then the whole value gets encoded.

For details see the *Syntax of encoded-words* section in [RFC 2047](https://www.ietf.org/rfc/rfc2047.txt).

## [Identification header](/docs/mdemail/6.4.1/operating/specific-email-headers#identification-header)

### [X-MD-Email-Security-Id](/docs/mdemail/6.4.1/operating/specific-email-headers#x-md-email-security-id)

This header contains the unique identifier of this email within MetaDefender Email Gateway Security.

## [Scan information headers](/docs/mdemail/6.4.1/operating/specific-email-headers#scan-information-headers)

### [X-Metadefender-Core-Url](/docs/mdemail/6.4.1/operating/specific-email-headers#x-metadefender-core-url)

This header contains the MetaDefender Core REST API URL used in scanning operations for this email.

Same value as in profile

This header will contain exactly the same value that is configured for the appropriate server in the applied server profile. For details about server profiles see: [Configuration/Server profiles](/docs/mdemail/6.4.1/configuration/server-profiles).

#### [Example](/docs/mdemail/6.4.1/operating/specific-email-headers#example)

**Server profile setting**

**Header**

`X-Metadefender-Core-URL: http://127.0.0.1:8008`

### [X-Metadefender-Core-Result](/docs/mdemail/6.4.1/operating/specific-email-headers#x-metadefender-core-result)

This header value will contain the MetaDefender Core process result. For Blocked results, the reason is also displayed (separated by a / character).

#### [Examples](/docs/mdemail/6.4.1/operating/specific-email-headers#examples)

| Header | Description |
| --- | --- |
| X-Metadefender-Core-Result: Allowed | None of the scan engines found a threat in the email and thus it was treated as clean. |
| X-Metadefender-Core-Result: Blocked/Dirty | Some (or all) of the scan engines found threat(s) in the email. |

### [X-Metadefender-EmailSecurity-Sanitized](/docs/mdemail/6.4.1/operating/specific-email-headers#x-metadefender-emailsecurity-sanitized)

This header is added to all emails indicating whether the email have been sanitized by the Email Gateway Security or not (header value: True or False ).

### [X-Metadefender-EmailSecurity-OriginalCopy](/docs/mdemail/6.4.1/operating/specific-email-headers#x-metadefender-emailsecurity-originalcopy)

This header is added to all original copies of blocked or sanitized emails (header value: True).

### [X-Metadefender-Core-Rule](/docs/mdemail/6.4.1/operating/specific-email-headers#x-metadefender-core-rule)

This header value will contain the name (or the value Automatic) of the MetaDefender Core rule that was configured to be used to scan this email. For details see [Configuration/Server profiles](/docs/mdemail/6.4.1/configuration/server-profiles).

#### [Examples](/docs/mdemail/6.4.1/operating/specific-email-headers#examples)

**Server profile setting**

**Header**

`X-Metadefender-Core-Rule: File scan`

**Server profile setting**

**Header**

`X-Metadefender-Core-Rule: Automatic`

## [External quarantine header](/docs/mdemail/6.4.1/operating/specific-email-headers#external-quarantine-header)

### [X-Metadefender-To-Quarantine](/docs/mdemail/6.4.1/operating/specific-email-headers#x-metadefender-to-quarantine)

If external quarantining is configured then this header is added to every email that is to be quarantined. For details see [Configuration/Quarantine configuration](/docs/mdemail/6.4.1/configuration/quarantine-configuration).

## [Custom headers](/docs/mdemail/6.4.1/operating/specific-email-headers#custom-headers)

In addition to the above headers, Email Gateway Security can also add custom headers (so called *X-headers*) to every email processed. These headers are configured in the security policy.

For details see [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy).

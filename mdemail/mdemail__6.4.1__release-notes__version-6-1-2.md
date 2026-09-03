<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/release-notes/version-6-1-2 -->

# Version 6.1.2

| Release date | Scope |
| --- | --- |
| 10th September, 2025 | Bug fixes and usability enhancements. |

## [New & improved](/docs/mdemail/6.4.1/release-notes/version-6-1-2#new--improved)

### [Import Security Rule filters, Blocklist and Trusted senders](/docs/mdemail/6.4.1/release-notes/version-6-1-2#import-security-rule-filters-blocklist-and-trusted-senders)

For easier administration it is now supported to import Security Rule filters, Blocklist and Trusted senders entries from files. The already configured values can be exported to files.

For details see [Trusted senders](/docs/mdemail/6.4.1/configuration/trustedsenders#importing-from-csv), [Blocklist](/docs/mdemail/6.4.1/configuration/blocklist#importing-from-csv) and [Policy](/docs/mdemail/6.4.1/configuration/policy#importing-from-csv).

### [User guide chatbot](/docs/mdemail/6.4.1/release-notes/version-6-1-2#user-guide-chatbot)

A chatbot has been introduced that can assist administrators with administrator guide searches.

Trained on the administrator guide

The chatbot is trained on the user guide only and it supports searching and summarizing the user guide only.

The chatbot is not capable to provide admins with direct configuration changes or other direct operations.

### [Added TNEF sanitization support](/docs/mdemail/6.4.1/release-notes/version-6-1-2#added-tnef-sanitization-support)

MetaDefender Core has been supporting [Transport Neutral Encapsulation Format (TNEF)](https://en.wikipedia.org/wiki/Transport_Neutral_Encapsulation_Format) sanitization.

When TNEF was converted during the sanitization, Email Gateway Security did not accept the converted TNEF file as the email body.

Accepting converted TNEF as a body has been added to the product.

### [Filter by Security Rule](/docs/mdemail/6.4.1/release-notes/version-6-1-2#filter-by-security-rule)

Filtering the Email History and Quarantine supports now the Security Rule that processed the email.

For details see [Filtering](/docs/mdemail/6.4.1/operating/email-history#filtering).

### [Increased length of Quarantine](/docs/mdemail/6.4.1/release-notes/version-6-1-2#increased-length-of-quarantine)

Email History, Refused Emails and Quarantine lists now support entries on a single page up to 250. This way bulk operations can now be performed on more entries than before (previously the list length topped at 100).

For details see [User settings](/docs/mdemail/6.4.1/configuration/users#user-settings).

### [External Core load balancing](/docs/mdemail/6.4.1/release-notes/version-6-1-2#external-core-load-balancing)

MetaDefender Core can be configured to return its IP address or FQDN in the newly added `X-Core-Id` custom response header. This header can be used to create a direct link to the scan result, bypassing the load balancer and ensuring that the request is directed to the Core server that processed the email.

For details see [Use X-Core-Id header for scan URLs](/docs/mdemail/6.4.1/configuration/settings#use-x-core-id-header-for-scan-urls).

## [Fixed](/docs/mdemail/6.4.1/release-notes/version-6-1-2#fixed)

### [Insufficient memory](/docs/mdemail/6.4.1/release-notes/version-6-1-2#insufficient-memory)

Certain emails could cause Email Gateway Security service to restart with errors complaining about *insufficient memory*.

### [AD group logins failed](/docs/mdemail/6.4.1/release-notes/version-6-1-2#ad-group-logins-failed)

When management console users were added to the system through Active Directory (AD) groups, the users were unable to log in.

### [From headers dropped](/docs/mdemail/6.4.1/release-notes/version-6-1-2#from-headers-dropped)

For certain emails Email Gateway Security dropped the `From` header.

### [Emails only in Quarantine](/docs/mdemail/6.4.1/release-notes/version-6-1-2#emails-only-in-quarantine)

In certain cases quarantined emails did not show up in the Email History, only in the Quarantine.

### [Monosign SSO error](/docs/mdemail/6.4.1/release-notes/version-6-1-2#monosign-sso-error)

Due to errors on the service provider side, Monosign SSO did not work in certain cases. The service provider has fixed the issue and Email Gateway Security has the documentation for the specific settings needed for this provider.

For details see the *Monosign example* section in [OpenID Connect](/docs/mdemail/6.4.1/configuration/users#openid-connect).

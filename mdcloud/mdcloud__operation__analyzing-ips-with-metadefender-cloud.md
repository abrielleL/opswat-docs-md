<!-- source: https://www.opswat.com/docs/mdcloud/operation/analyzing-ips-with-metadefender-cloud -->

# Analyzing IPs with MetaDefender Cloud

## [About](/docs/mdcloud/operation/analyzing-ips-with-metadefender-cloud#about)

MetaDefender Cloud allows users to check IP addresses and domains for malicious behavior using many IP and domain reputation sources. This functionality makes it possible to identify threats like botnets or phishing sites that would not be found through scanning files when accessing content. By providing a standardized interface for the leading IP reputation sources, MetaDefender Cloud aggregates data on whether an IP, domain or URL address should be trusted.

The potential maliciousness of an IP address or domain can change frequently. To keep our results up-to-date and reduce false positives, we only save our results from the IP reputation sources for 15 days.

The scan result for each provider will follow this sample structure:

{
"provider": "webroot.com",
"assessment": "trustworthy",
"category": "Business and Economy;Computer and Internet Info",
"detect_time": "",
"update_time": "2020-11-20T16:25:30.772Z",
"status": 0
},

Below are additional explanations for the scan results we return for IP addresses and domains.

## [Providers](/docs/mdcloud/operation/analyzing-ips-with-metadefender-cloud#providers)

We are currently using many sources to collect malicious addresses. Below is a list of the sources that MetaDefender Cloud currently incorporates. This list is subject to change depending on the availability and reliability of its contents.

- [alexa.com](http://alexa.com)
- [apwg.org](http://apwg.org)
- [autoshun.org](http://autoshun.org)
- [blocklist.de](http://blocklist.de)
- [botscout.com](http://botscout.com)
- [csirtg.io](http://csirtg.io)
- [danger.rulez.sk](http://danger.rulez.sk)
- [darklist.de](http://darklist.de)
- [dataplane.org](http://dataplane.org)
- [emergingthreats.net](http://emergingthreats.net)
- [feodotracker.abuse.ch](http://feodotracker.abuse.ch)
- [isc.sans.edu](http://isc.sans.edu)
- [malwaredomains.com](http://malwaredomains.com)
- [mirc.com](http://mirc.com)
- [NormShield.com](http://NormShield.com)
- [nothink.org](http://nothink.org)
- [openphish.com](http://openphish.com)
- [osint.bambenekconsulting.com](http://osint.bambenekconsulting.com)
- [ransomwaretracker.abuse.ch](http://ransomwaretracker.abuse.ch)
- [reputation.alienvault.com](http://reputation.alienvault.com)
- [sblam.com](http://sblam.com)
- [spamhaus.org](http://spamhaus.org)
- [sslbl.abuse.ch](http://sslbl.abuse.ch)
- [stopforumspam.com](http://stopforumspam.com)
- [torproject.org](http://torproject.org)
- [umbrella.cisco.com](http://umbrella.cisco.com)
- [urlhaus.abuse.ch](http://urlhaus.abuse.ch)
- [vxvault.net](http://vxvault.net)
- [Webroot Web Classification and Web Reputation](https://www.webroot.com/us/en/business/threat-intelligence/internet/web-classification-and-reputation-services) and [IP reputation](https://www.webroot.com/us/en/business/threat-intelligence/internet/ip-reputation) ,

## [Status](/docs/mdcloud/operation/analyzing-ips-with-metadefender-cloud#status)

There are three possible results for each of the sources listed below. MetaDefender Cloud will categorize anything as **Blocklisted** if it is reported as malicious by any of the sources. Our policy is to keep these up to 15 days in order to limit potential false positives.

See more details about our expiration policy in the Last Detected section.

| **0** | Allowlisted**:** IP is listed by the source in their allowlist. **Note:** Not all sources provide allowlists. |
| --- | --- |
| **1** | Blocklisted**:** IP is listed by the source in their blocklist. Refer to the source for more information regarding their blocklist. |
| **3** | **Failed to scan:** The results could not be retrieved from our servers |
| **5** | **Unknown:** The source has not listed this IP address in either their blocklist or allowlist. |

## [Last Updated](/docs/mdcloud/operation/analyzing-ips-with-metadefender-cloud#last-updated)

Currently, MetaDefender Cloud's IP-Domain database is updated daily for each source, which is indicated in the "update_time" field of the results. However, this does not necessarily correspond directly with the source releasing their own list.

## [Last Detected](/docs/mdcloud/operation/analyzing-ips-with-metadefender-cloud#last-detected)

The "detect_time" indicates the last time an IP address was confirmed as belonging to a feed. There are two different types of feed (i.e., blocklist or allowlist). One is reset with only active bad IPs and the other is accumulated with newly-found bad IPs.

## [Assessment](/docs/mdcloud/operation/analyzing-ips-with-metadefender-cloud#assessment)

MetaDefender Cloud utilizes the assessments below:

| **Assessment** | **Description** |
| --- | --- |
| **botnet** | - Typically a host used to control another host or malicious process. - Matching traffic would usually indicate infection. - Typically used to identify compromised hosts. |
| **malware** | - Typically a host used to exploit and/or drop malware to a host for the first time. - Typically NOT a botnet controller (although they could overlap). - Communications with these indicators may lead to a compromise and then to a possible botnet controller communication (if the infection was successful). - Typically used in preemptive blocking, alerts may not indicate infection was successful. |
| **phishing** | - A luring attempt at a victim to exfiltrate some sort of credential. - A targeted attempt at getting someone to unintentionally cause infection (spear phishing). |
| **scanner** | - Typically infrastructure being used to scan or brute-force (SSH, RDP, telnet, etc...). |
| **spam** | - Typically infrastructure being used to facilitate the sending of spam. |
| **suspicious** | - There are reasons to believe this address might be conducting malicious activity |
| **bruteforce** | - Such addresses have been used to conduct bruteforce password checking on login pages |
| **tor** | - The address has been spotted on the "tor" network |
| **blocklist** | - This address has been included in a blocklist for unspecified reasons |
| **high risk** | - Highly risky address |
| **trustworthy** | - Denotes that a specific entity (usually an address) should be considered harmless in nature. - Denotes that blocking an entity would result in mass collateral damage (e.g., Yahoo virtually-hosted services). |

## [Category](/docs/mdcloud/operation/analyzing-ips-with-metadefender-cloud#category)

This is a classification of the website. Each website can have multiple classifications depending on it's area of expertise. Category is not always returned, only some vendors provide URL/Domain classification.

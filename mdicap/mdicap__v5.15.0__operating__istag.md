<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/operating/istag -->

# ISTag

View as Markdown Ask ChatGPT about this page Ask Claude about this page

- [Overview](/docs/mdicap/v5.15.0/operating/istag#overview)
- [MetaDefender ICAP Server specific ISTag](/docs/mdicap/v5.15.0/operating/istag#metadefender-icap-server-specific-istag)

  - [Keeping the ISTag in sync among MetaDefender ICAP Server instances](/docs/mdicap/v5.15.0/operating/istag#keeping-the-istag-in-sync-among-metadefender-icap-server-instances)

## [Overview](/docs/mdicap/v5.15.0/operating/istag#overview)

The ISTag (ICAP Service Tag) response-header field provides a way for the ICAP server to send a service-specific *cookie* to ICAP clients that represents a service's current state. It is a maximum 32 byte alphanumeric string of data that may, for example, be a representation of the software version or configuration of the ICAP service. An ISTag validates that previous ICAP server responses can still be considered fresh by an ICAP client that may be caching them. If a change on the ICAP server invalidates previous responses, the ICAP server can invalidate portions of the ICAP client's cache by changing its ISTag. [<https://tools.ietf.org/html/rfc3507#section-4.7>]

For example, considering a virus-scanning ICAP service, the ISTag might be a combination of the virus scanner's software version and the release number of its virus signature database. When the database is updated, the ISTag can be changed to invalidate all previous responses that had been certified as clean and cached with the old ISTag. [<https://tools.ietf.org/html/rfc3507#section-4.7>]

## [MetaDefender ICAP Server specific ISTag](/docs/mdicap/v5.15.0/operating/istag#metadefender-icap-server-specific-istag)

In MetaDefender ICAP Server the ISTag represents the last time, when it had to be changed.

Depending on the configuration, the ISTag is forced to change with one of the following frequencies:

- per minute,
- hourly or
- daily.

For details see [Tuning](/docs/mdicap/v5.15.0/configuration/additional-tuning).

Info

**Time drift**

ICAP Server’s ISTag generation mechanism is protected against minor drifts of the actual time of the generation of the ISTag.

IT means, that for example when the ISTag update frequency is *hourly* and the actual generation -due to high load for example- happens at 2020-04-28 10:00:**03**, still the ISTAg will represent 2020-04-28 10:00:**00**

## [Keeping the ISTag in sync among MetaDefender ICAP Server instances](/docs/mdicap/v5.15.0/operating/istag#keeping-the-istag-in-sync-among-metadefender-icap-server-instances)

Info

**The problem**

For performance and stability reasons, some ICAP clients recommend deploying multiple ICAP servers. If these ICAP servers run in parallel, but their ISTags differ (and the ICAP client does not register which cache entry belongs to which ICAP server), then the ICAP servers will continuously invalidate each others' scan results.

As in MetaDefender ICAP Server the ISTag represents the time, when the ISTag was last changed, the following requirements must be fulfilled to keep the ISTag in sync among ICAP Server instances:

1. The clock of the ICAP Servers must be in sync,
2. All ICAP Servers' clocks must be configured for the same time zone,
3. All ICAP Servers must be configured for the same *istag_frequency* (see [Tuning](/docs/mdicap/v5.15.0/configuration/additional-tuning)).

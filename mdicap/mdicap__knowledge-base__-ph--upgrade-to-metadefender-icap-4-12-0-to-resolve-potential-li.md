<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/-ph--upgrade-to-metadefender-icap-4-12-0-to-resolve-potential-li -->

# How do I resolve potential licensing errors after March 2022?

This article applies to Windows or Linux systems running MetaDefender ICAP Server V4.11.1 or older only.

Please Note:

Since March 2022, users running MetaDefender ICAP Server V4.11.1 are likely to encounter licensing errors when attempting to add an ICAP Server license renewal to their system.

This issue should not occur under normal day-to-day usage. However, OPSWAT still highly recommends that users upgrade to the latest version of ICAP Server before attempting to add a license renewal.

Beginning with V4.12.0, and in order to streamline the licensing process, MetaDefender ICAP Server’s licensing engine no longer counts client IPs (i.e., the number of clients that are allowed to send data to the ICAP Server).

- The removal of this checking function aligns the MetaDefender ICAP Server with the licensing of other OPSWAT products, providing customers with enhanced flexibility when deploying and managing their security environment.
- Beginning with MetaDefender ICAP Server V4.12.0, the licensing engine only counts the number of deployments or activations.

The error, which is resolved by upgrading to the latest version of MetaDefender ICAP Server, is illustrated in the screenshot below:

Error

Message Infected - rejecting message. Threat: X-Response-Info: Blocked X-Response-Desc: **Missing client IP**.

As a part of this streamlining process, OPSWAT also implemented enhancements to their backend licensing server in March 2022, and while this is not directly related to the engine upgrades mentioned above, it may lead to similar errors when adding a license renewal.

As above, this error can be resolved by upgrading to the latest version of MetaDefender ICAP Server. For details on the latest ICAP Server release [Read This](/docs/mdicap/release-notes/release-notes).

Pro Tip:

OPSWAT highly recommends that users regularly upgrade to the latest version of MetaDefender ICAP Server and not wait until the end of a release’s support cycle.

Current versions incorporate state-of-the-art features and necessary bug fixes, and are freely available for all license holders to download.

Support:

Should you **Encounter This Error Outside Of The Scenarios Described Above**, please open a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).

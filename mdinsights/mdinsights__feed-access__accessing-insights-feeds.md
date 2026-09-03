<!-- source: https://www.opswat.com/docs/mdinsights/feed-access/accessing-insights-feeds -->

[MetaDefender InSights](https://www.opswat.com/docs/mdinsights)Need Help? [Contact Support](https://www.opswat.com/support/contact-support)
# Accessing InSights Feeds

MetaDefender InSights is accessible through multiple channels. Below we provide an overview of these options.

## [Flexible Data Access Methods](/docs/mdinsights/feed-access/accessing-insights-feeds#flexible-data-access-methods)

InSights threat intelligence data is available in multiple access methods to satisfy a variety of needs and use cases.

### [API lookups](/docs/mdinsights/feed-access/accessing-insights-feeds#api-lookups)

InSights threat intelligence data may be leveraged by integrators to query for indicators and enrich data on demand in web applications, chat interfaces, SOAR platforms, and more. OPSWAT provides a RESTful JSON web API and offers multiple tiers of query rates to meet your needs. Newly released indicators are exposed via the API immediately and will be returned in queries without delay. This query interface is available through OPSWAT's MetaDefender InSights [API Access](/docs/mdinsights/feed-access/api).

### [Bulk intelligence data downloads (snapshots)](/docs/mdinsights/feed-access/accessing-insights-feeds#bulk-intelligence-data-downloads-snapshots)

InSights threat intelligence snapshots provide a complete, downloadable collection of active threat indicators. Snapshots are designed for those that wish to load threat intelligence data into their own data stores for flexible integration options. This is useful for organizations that aggregate threat indicators into their own threat intelligence platfoms (TIPs), SIEMs or data lakes. Snapshots contain the most recently available active indicators; indicators that have already reached their expiration date or have otherwise aged out are not included in the most recent snapshots. Snapshots are updated hourly to ensure rapid access to new indicators, and customers are advised to only attempt to download them as often as once per hour. This is available through OPSWAT's MetaDefender InSights [API Access](/docs/mdinsights/feed-access/api).

### [Threat Intelligence Platform (TIP) partner integrations](/docs/mdinsights/feed-access/accessing-insights-feeds#threat-intelligence-platform-tip-partner-integrations)

MetaDefender InSights threat intelligence data is integrated today in exclusive partner intelligence portals. See [Partner Availability](/docs/mdinsights/feed-access/partner-access) for further details.

  Last updated  on  Next to read:  [API Access](/docs/mdinsights/feed-access/api) On This Page [Accessing InSights Feeds](https://www.opswat.com/docs/mdinsights/feed-access/accessing-insights-feeds#)[Flexible Data Access Methods](https://www.opswat.com/docs/mdinsights/feed-access/accessing-insights-feeds#flexible-data-access-methods)[API lookups](https://www.opswat.com/docs/mdinsights/feed-access/accessing-insights-feeds#api-lookups)[Bulk intelligence data downloads (snapshots)](https://www.opswat.com/docs/mdinsights/feed-access/accessing-insights-feeds#bulk-intelligence-data-downloads-snapshots)[Threat Intelligence Platform (TIP) partner integrations](https://www.opswat.com/docs/mdinsights/feed-access/accessing-insights-feeds#threat-intelligence-platform-tip-partner-integrations)

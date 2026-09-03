<!-- source: https://www.opswat.com/docs/mdinsights/feed-access/api -->

[MetaDefender InSights](https://www.opswat.com/docs/mdinsights)Need Help? [Contact Support](https://www.opswat.com/support/contact-support)
# API Access

MetaDefender InSights is accessible via a RESTful web API that presents threat intelligence indicators in a simple JSON data format.

API Client

This page documents the API for accessing threat intelligence feed data. For users that would prefer a simpler way of accessing MetaDefender InSights data snapshots, we also offer a Python [API Client](/docs/mdinsights/feed-access/api-client).

## [Authentication and authorization](/docs/mdinsights/feed-access/api#authentication-and-authorization)

API access is available using an API key. The API key is passed to the server in the request body as a parameter named `api_key`. Customer API keys are granted access to individual API endpoints and must be authorized to retrieve InSights threat intel data.

## [How to query the API](/docs/mdinsights/feed-access/api#how-to-query-the-api)

API access details:

- **API host**: <https://eyelet.inquest.net>
- **API authentication**: API queries must be authenticated, and require an API key to identify the requestor.

To query the APIs documented on this page:

1. Send an HTTPS request to the URL of the desired API endpoint.
2. Send requests using the `POST` method.
3. Include the API key in a form-encoded request body.

For example, to download the **MetaDefender InSights C2 domain feed** in Python using [Requests](https://requests.readthedocs.io/en/stable/), assuming that a valid API key is in the `INSIGHTS_API_KEY` environment variable:

PythonCopyimport os
import requests
API_HOST = "https://eyelet.inquest.net"
API_KEY = os.environ["INSIGHTS_API_KEY"]
r = requests.post(
f"{API_HOST}/api/insights/insights-c2-domain", data={"api_key": API_KEY}
)
with open("inquest-insights-c2-ip.json.gz", "wb") as f:
f.write(r.content)
## [Lookup query interface](/docs/mdinsights/feed-access/api#lookup-query-interface)

### [Supported InSights data feeds](/docs/mdinsights/feed-access/api#supported-insights-data-feeds)

Data from the following MetaDefender InSights feeds are available through the lookup query interface:

- [MetaDefender InSights C2](/docs/mdinsights/feeds/metadefender-insights-c2)
- [MetaDefender InSights TI](/docs/mdinsights/feeds/metadefender-insights-ti)

### [Supported API endpoints](/docs/mdinsights/feed-access/api#supported-api-endpoints)

The following API endpoints are supported through the query interface:

---

#### [InSights C2 DNS lookup](/docs/mdinsights/feed-access/api#insights-c2-dns-lookup)

| Endpoint URI path | Description |
| --- | --- |
| `/c2/dns/query` | Query the MetaDefender InSights C2 API to determine if any supplied domain name artifacts are identified as C2 endpoints. |

---

#### [InSights C2 IP lookup](/docs/mdinsights/feed-access/api#insights-c2-ip-lookup)

| Endpoint URI path | Description |
| --- | --- |
| `/c2/ip/query` | Query the the MetaDefender InSights C2 API to determine if any supplied IP address artifacts are identified as C2 endpoints. |

---

#### [InSights TI reputation lookup](/docs/mdinsights/feed-access/api#insights-ti-reputation-lookup)

| Endpoint URI path | Description |
| --- | --- |
| `/rep/query` | Query the the MetaDefender InSights TI and InQuest Labs reputation API to determine if any supplied IP/domain artifacts are identified as having a bad reputation. |

---

## [Download interface](/docs/mdinsights/feed-access/api#download-interface)

Our threat intelligence feeds may be downloaded in a packaged bulk format to support raw data use cases. The feed collections consist of the subset of our active threat indicators that have not yet aged out due to expiration, and help ensure that our customers receive actionable, relevant insights. We refer to these bulk intel data collections as ***snapshots***.

### [Supported InSights data feeds](/docs/mdinsights/feed-access/api#supported-insights-data-feeds)

The following MetaDefender InSights data feeds are available through the snapshot download interface:

- [MetaDefender InSights C2](/docs/mdinsights/feeds/metadefender-insights-c2)
- [MetaDefender InSights TI](/docs/mdinsights/feeds/metadefender-insights-ti)
- [MetaDefender InSights OSINT](/docs/mdinsights/feeds/metadefender-insights-osint)

### [Supported API endpoints](/docs/mdinsights/feed-access/api#supported-api-endpoints)

The following API endpoints can be accessed through the snapshot download interface:

---

#### [InSights C2 snapshots](/docs/mdinsights/feed-access/api#insights-c2-snapshots)

| Endpoint URI path | Description |
| --- | --- |
| `/api/insights/insights-c2-ip` | Download the most recent MetaDefender InSights C2 IP address feed snapshot. |
| `/api/insights/insights-c2-domain` | Download the most recent MetaDefender InSights C2 DNS feed. |

---

#### [InSights TI snapshots](/docs/mdinsights/feed-access/api#insights-ti-snapshots)

| Endpoint URI path | Description |
| --- | --- |
| `/api/insights/insights-ti-ip` | Download the most recent MetaDefender InSights TI IP address feed snapshot. |
| `/api/insights/insights-ti-domain` | Download the most recent MetaDefender InSights TI DNS feed snapshot. |
| `/api/insights/insights-ti-url` | Download the most recent MetaDefender InSights TI URL feed snapshot. |

---

#### [InSights OSINT snapshots](/docs/mdinsights/feed-access/api#insights-osint-snapshots)

| Endpoint URI path | Description |
| --- | --- |
| `/api/insights/insights-osint-domain` | Download the most recent MetaDefender InSights OSINT domain feed snapshot. |

---

  Last updated  on  Next to read:  [Partner Availability](/docs/mdinsights/feed-access/partner-access) On This Page [API Access](https://www.opswat.com/docs/mdinsights/feed-access/api#)[Authentication and authorization](https://www.opswat.com/docs/mdinsights/feed-access/api#authentication-and-authorization)[How to query the API](https://www.opswat.com/docs/mdinsights/feed-access/api#how-to-query-the-api)[Lookup query interface](https://www.opswat.com/docs/mdinsights/feed-access/api#lookup-query-interface)[Supported InSights data feeds](https://www.opswat.com/docs/mdinsights/feed-access/api#supported-insights-data-feeds)[Supported API endpoints](https://www.opswat.com/docs/mdinsights/feed-access/api#supported-api-endpoints)[InSights C2 DNS lookup](https://www.opswat.com/docs/mdinsights/feed-access/api#insights-c2-dns-lookup)[InSights C2 IP lookup](https://www.opswat.com/docs/mdinsights/feed-access/api#insights-c2-ip-lookup)[InSights TI reputation lookup](https://www.opswat.com/docs/mdinsights/feed-access/api#insights-ti-reputation-lookup)[Download interface](https://www.opswat.com/docs/mdinsights/feed-access/api#download-interface)[Supported InSights data feeds](https://www.opswat.com/docs/mdinsights/feed-access/api#supported-insights-data-feeds)[Supported API endpoints](https://www.opswat.com/docs/mdinsights/feed-access/api#supported-api-endpoints)[InSights C2 snapshots](https://www.opswat.com/docs/mdinsights/feed-access/api#insights-c2-snapshots)[InSights TI snapshots](https://www.opswat.com/docs/mdinsights/feed-access/api#insights-ti-snapshots)[InSights OSINT snapshots](https://www.opswat.com/docs/mdinsights/feed-access/api#insights-osint-snapshots)

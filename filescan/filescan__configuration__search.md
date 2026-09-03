<!-- source: https://www.opswat.com/docs/filescan/configuration/search -->

# Search

In the **Admin Panel > Settings > Configuration > Search** section, settings related to search can be specified. Restrictions related to the number of reports and their age can be set for different user levels.

Search settings under Configuration

### [Configuration options](/docs/filescan/configuration/search#configuration-options)

| Fields | Description |
| --- | --- |
| `SEARCH_REPORTS_LIMIT` | This field sets the maximum number of reports returned by the search (not limited if the value is 0) |
| `SEARCH_REPORTS_LIMIT_PREVALENCE` | Limits the maximum number of similar reports to search for related to the IOCs. (not limited if the value is 0) |
| `SEARCH_MONTHS_LIMIT_GUEST` | It can be configured to return results going back how many months for guest users. (not limited if the value is 0) |
| `SEARCH_MONTHS_LIMIT_USER` | It can be configured to return results going back how many months for normal users. (not limited if the value is 0) |
| `SEARCH_MONTHS_LIMIT_ADMIN` | It can be configured to return results going back how many months for Admin users. (not limited if the value is 0) |
| `SEARCH_MONTHS_LIMIT_INTEL` | It can be configured to return results going back how many months for Intel users. (not limited if the value is 0) |
| `SEARCH_MONTHS_LIMIT_PREVALENCE` | How many months back to search for similar reports. (not limited if the value is 0) |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

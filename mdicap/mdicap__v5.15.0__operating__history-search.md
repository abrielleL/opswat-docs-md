<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/operating/history-search -->

# History Search

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Filtering columns](/docs/mdicap/v5.15.0/operating/history-search#filtering-columns)

By clicking on the "Advanced" button icon

A new popup will appear with filters for the given rows.

Using these filters you can search for ICAP requests which have to meet multiple criteria e.g. request where the action was BLOCKED and the client IP was 127.0.0.1 at the same time. This indicates that there is **AND** relation between the filters.

### [Enable/disable hidden column](/docs/mdicap/v5.15.0/operating/history-search#enabledisable-hidden-column)

be default, below column are hidden, these columns can be configured by check/uncheck the option of each column at the dropdown option.

- **User Name**: This is for Filemod feature, supported since v5.1.0
- **Host**: When enable, the Host can be filtered, supported since v5.2.1

## [Tokenization](/docs/mdicap/v5.15.0/operating/history-search#tokenization)

When using text filters, like *Result* you would expect that writing "Ba" in the filter would return every rows with "Bad request" result however this is not the case since the search is based on tokens. If you would like to get the requests with result "Bad request" you would have to write "Ba*" or "Bad" as the filter string.

## [Value only search](/docs/mdicap/v5.15.0/operating/history-search#value-only-search)

By default it is possible to search for a certain value among the values of all columns.

## [Example](/docs/mdicap/v5.15.0/operating/history-search#example)

### [List](/docs/mdicap/v5.15.0/operating/history-search#list)

| ID | RESULT | STATUS |
| --- | --- | --- |
| 1 | ALLOWED | BLOCKED |
| 2 | BLOCKED | COMPLETED |

### [Search results](/docs/mdicap/v5.15.0/operating/history-search#search-results)

| Search term | Matching rows |
| --- | --- |
| BLOCKED | 1, 2 |

## [Lists with value only search](/docs/mdicap/v5.15.0/operating/history-search#lists-with-value-only-search)

The following lists in ICAP Server implement value only search:

1. **Dashboard > Config history**

## [Full text search (FTS)](/docs/mdicap/v5.15.0/operating/history-search#full-text-search-fts)

MetaDefender ICAP Server implements the SQLite MATCH feature of [SQLite FTS3 and FTS4 Extensions](https://www.sqlite.org/fts3.html) (see section *3. Full-text Index Queries*). In addition to the capabilities the value only search provides, using the MATCH feature makes it possible to search for certain values in certain fields.

Info

From v5.2.0, the SQLite has already replaced by PostgreSQL

## [Example](/docs/mdicap/v5.15.0/operating/history-search#example)

### [List](/docs/mdicap/v5.15.0/operating/history-search#list)

| ID | RESULT | STATUS |
| --- | --- | --- |
| 1 | ALLOWED | BLOCKED |
| 2 | BLOCKED | COMPLETED |
| 3 | NOT BLOCKED | COMPLETED |
| 4 | BLOWN | BLOCKED |

### [Search results](/docs/mdicap/v5.15.0/operating/history-search#search-results)

| Search term | Matching rows |
| --- | --- |
| BLOCKED | 1, 2 |
| RESULT:BLOCKED | 1, 3 |
| RESULT:^BLOCKED | 1 |
| RESULT:BLO* | 1, 3, 4 |
| RESULT:^BLO* | 1, 4 |

Success

For a more complete reference of possible search terms see <https://www.sqlite.org/fts3.html>.

## [Lists with FTS](/docs/mdicap/v5.15.0/operating/history-search#lists-with-fts)

The following lists in ICAP Server implement full text search:

1. **Dashboard > ICAP history**

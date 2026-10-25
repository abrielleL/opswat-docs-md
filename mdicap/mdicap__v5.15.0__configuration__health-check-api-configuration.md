<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/configuration/health-check-api-configuration -->

# Health Check API Configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page Product version supported

MetaDefender ICAP Server version 5.1.1 or newer

Health check API feature supports you to verify MetaDefender ICAP Server application readiness.

The readiness condition is determined via product configurations, see more at [Configure health check policy](/docs/mdicap/v5.15.0/configuration/health-check-api-configuration#configure-health-check-policy).

## [Using the health check API](/docs/mdicap/v5.15.0/configuration/health-check-api-configuration#using-the-health-check-api)

Health check API expects to return HTTP(S) 200 Successful only when all pre-configured conditions met.

**Request:**

| Method | URL | Auth | Function |
| --- | --- | --- | --- |
| GET | /readyz | None | Heath check endpoint |

**Request query params :**

| Name | Type | Detail | Required |
| --- | --- | --- | --- |
| verbose | Boolean | Show detailed result of health check | no |

**Response** **status code:**

| HTTP status code | Description |
| --- | --- |
| 200 | Healthy. ICAP service is fully up and running, and ready for process request |
| 503 | Not healthy. ICAP service is not ready to handle any request yet or got issues |
| 500 | ICAP service is down. Internal Server Error |

**Response body (only response when verbose enabled)**

| **Json element** |  | **type** | Description | Support from |
| --- | --- | --- | --- | --- |
| **database** |  | object | Database connection | 5.1.1 |
|  | status | string | Database connection status true/false |  |
| **license** |  |  |  | 5.1.1 |
|  | status | string | License status  `expired`,`invalid`,`ok` |  |
| **server_profiles** |  |  | The status of server profiles | 5.2.1 |
|  | required | Boolean | Indicate whether the status of server profiles checking affects the final result or not |  |
|  | status | Boolean | The connection status between the ICAP Server and the Scan Server (MD-Core, MD-Cloud)   - true: healthy - false: unhealthy |  |
| **engines** |  | object | The status of ICAP Server's engines | 5.10.0 |
| **engines.filetype** |  | object | The status of the FileType engines | 5.10.0 |
|  | required | Boolean | Indicate whether the status of the FileType engine checking affects the final result or not |  |
|  | status | Boolean | The status of the FileType engine   - true: healthy - false: unhealthy |  |

**Example:**

curl --request GET --url 'http://localhost:8048/readyz?verbose=true'{
"database": {
"status": true
},
"license": {
"status": "ok"
},
"server_profiles": {
"required": true,
"status": true
},
"engines": {
"filetype": {
"required": true,
"status": true
}
}
}
## [Configure health check policy](/docs/mdicap/v5.15.0/configuration/health-check-api-configuration#configure-health-check-policy)

You are supported to adjust thresholds on vital criterias as your own policy tailored for heath check verification, via both REST API and MetaDefender ICAP Server management console.

### [Using UI](/docs/mdicap/v5.15.0/configuration/health-check-api-configuration#using-ui)

The relevant settings could be found under S**ettings > System > Health Check**

|  | Value | Description | Support from |
| --- | --- | --- | --- |
| **Enable Health Check** | On / Off | Enabling this option will allow MetaDefender ICAP Server automatically run a background task to collect application operational data for health check logic. | 5.1.1 |
| **Check Server Profiles** | On / Off | Defines if server profile availability should be considered for health status. | 5.2.1 |
|  | **Condition** | Defines when to report unhealthy status:  `- "Any profile is unavailable"`: If **any** profile is unavailable, report unhealthy.  `- "All profiles are unavailable"`: Only report unhealthy if **all** profiles are unavailable. |  |
| **Check FileType Engine** | On / Off | If `true`, the FileType engine availability will be included in the health check evaluation. | 5.10.0 |

### [Using administrative REST API](/docs/mdicap/v5.15.0/configuration/health-check-api-configuration#using-administrative-rest-api)

**Get setting heath check**

**Request:**

| Method | URL | Auth | Function |
| --- | --- | --- | --- |
| GET | /admin/config/healthcheck | Administrator | Heath check endpoint |

**Response Body:**

- `enable_feature` enable or disable this feature
- `database`: true - always enable when enabled `enable_feature`
- `license`: true - always enable when enabled `enable_feature`
- `server_profiles`

  - `enable` enable or disable this feature
  - `config`

    - `check_all_rules`:

      - true : /readyz will return status code 503 if **ALL** MD Core rules are not available (mean: all MD Core connect to ICAP are down or ALL MD Core rules are deleted from MD Core)
      - false : /readyz will return status code 503 if **ALL** MD Core rules are not available (mean: all MD Core connect to ICAP are down or ALL MD Core rules are deleted from MD Core)
- `engines`

  - `filetype`

    - `enable` enable or disable this feature

Example:

JsonCopy{
"enable_feature": true,
"database": true,
"license": true,
"server_profiles": {
"config": {
"check_all_profiles": true
},
"enable": true
},
"engines": {
"filetype": {
"enable": true
}
}
}

**Set setting heath check**

**Request:**

| Method | URL | Auth | Function |
| --- | --- | --- | --- |
| POST | /admin/config/healthcheck | Administrator | Set setting heath check |

**Request headers**

| Key | Value |
| --- | --- |
| apikey | Administrator's API Key |

**Request body:**

- `enable_feature` enable or disable this feature
- `server_profiles`

  - `enable` enable or disable this feature (default: **false**)
  - `config`

    - `check_all_rules`: (default: **false**)

      - true : /readyz will return status code 503 if **ALL** MD Core rules are not available (mean: all MD Core connect to ICAP are down or ALL MD Core rules are deleted from MD Core)
      - false : /readyz will return status code 503 if **ALL** MD Core rules are not available (mean: all MD Core connect to ICAP are down or ALL MD Core rules are deleted from MD Core)
- `engines`

  - `filetype`

    - `enable` enable or disable this feature (default: **false**)

Example:

JsonCopy{
"enable_feature": true,
"server_profiles": {
"config": {
"check_all_profiles": true
},
"enable": true
},
"engines": {
"filetype": {
"enable": true
}
}
}Info

From ICAP Server 5.2.1 the `core_rules` and `core_rules.config` have been replaced by `server_profiles` to make the API more friendly. The `core_rules` and `core_rules.config` still responds in the API for backward compatibility purposes, but we do not recommend using it.

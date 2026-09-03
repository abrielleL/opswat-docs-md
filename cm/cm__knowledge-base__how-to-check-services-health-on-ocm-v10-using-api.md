<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-to-check-services-health-on-ocm-v10-using-api -->

# How to check Services Health on OCM v10 using API

> This article explains how to check the health monitoring status of services in **CM10** using the REST API and interpret the returned `healthStatus` values.

## **Overview**

You can retrieve the health status of all services via the Fusion Console API endpoint:

```http
GET /fusion/console/services
```

The `healthStatus` field in the response indicates the operational state of each service.

## **Prerequisites**

- Access to the CM10 Fusion Console (web interface or API endpoint).
- A valid Bearer token for authentication (obtained via login API, refer to [https://www.opswat.com/docs/cm/developer-guidelines/authentication](https://www.opswat.com/docs/cm/developer-guidelines/authentication)).
- The base URL of your CM10 environment

### **Step-by-Step: Checking Health Status via API**

1. Obtain Authentication Token: obtained via login API, refer to [https://www.opswat.com/docs/cm/developer-guidelines/authentication](https://www.opswat.com/docs/cm/developer-guidelines/authentication)
2. Call the Services API Endpoint: Use a GET request to fetch the list of services.

**Endpoint**

```http
http://<CM10-IP>:9000/fusion/console/services?page=1&limit=25&sort=lastSeen&order=asc
```

- page=1 & limit=25: Pagination (adjust as needed; increase limit for more results).
- sort=lastSeen&order=asc: Optional sorting (by last seen time).

**Headers **(required):

```http
Authorization: Bearer <your_token_here>
```

### **Example using Python**

```python
import requests

url = "http://10.40.192.40:9000/fusion/console/services?page=1&limit=25&sort=lastSeen&order=asc"

payload = {}
headers = {
  'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIU****FJYR-KA'  # Replace with real token
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

*Alternative using curl:*

```bash
curl -X GET "http://10.40.192.40:9000/fusion/console/services?page=1&limit=25&sort=lastSeen&order=asc" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIU..."
```

***Example JSON Response***

```json
{
    "total": 2,
    "items": [
        {
            "serviceID": "6989927c8a223f113e48ca82",
            "serviceName": "MSCW4****",
            "productType": "MDCORE",
            ...
            "healthStatus": "Unknown",
            ...
            "status": "CONNECTED",
            ...
        },
        {
            "serviceID": "69899b238a223f113e48ca85",
            "serviceName": "MSCWd*****",
            "productType": "MDCORE",
            ...
            "healthStatus": "Operational",
            ...
            "status": "PENDING",
            ...
        }
    ]
}
```

In this example, one of the MetaDefender Core "healthStatus" is "Operational".

**Best practice**: Alert/monitor when healthStatus is anything other than **Operational**

The `healthStatus` value indicates the current operational state of a service. Below is a breakdown of all possible Health Status types and what each one means.

| Health Status | Description |
| ---- | ---- |
| **Operational** | The instance is fully operational and healthy. |
| **Minor Issues** | One or more warnings exist, but normal operations are not affected. |
| **Significant Issues** | The instance has major warnings that may impact operations if not addressed. |
| **Critical Issues** | Critical warnings exist; operations are impacted. Immediate action needed. |
| **Blocker Issues** | The instance has stopped functioning. Immediate action required. |
| **Unknown** | The instance has not yet reported its health stat |

> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

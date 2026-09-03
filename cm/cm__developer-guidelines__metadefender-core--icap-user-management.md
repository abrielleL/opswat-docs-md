<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/metadefender-core--icap-user-management -->

# MetaDefender Core, ICAP User Management

MetaDefender CORE and ICAP have built-in capabilities to manage users directly within each product instance. For example, administrators can create a user by sending an API request directly to a MetaDefender CORE instance.

This is an MetaDefender Core API to get all users:

```javascript
curl --get \
 --url 'http://localhost:8008/admin/user' \
 --header 'apikey: {apikey}'
```

However, this requires either local access to the instance or a network connection to it. If the administrator is on a different network, direct access may not be possible.

To overcome this limitation, administrators can enroll the MetaDefender CORE instance into **My OPSWAT Central Management** and perform the API through My OPSWAT Central Management as below:

```javascript
curl -X POST --location 'https://product.my.us.opswat.com/fusion/console/services/connection/{{CONNECTION_ID}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
--header 'X-App-Method: GET' \
--header 'X-App-URL: /admin/user'
```

Here are steps

**Step 1:** Enroll the MetaDefender CORE instance into My OPSWAT Central Management and obtain the Deployment Id.

![](https://uploads.developerhub.io/prod/97qW/h4il04427odqofd20lg6f2w256tml4da4k8xfkfyq4j5elbjlm1lz0f5adhar6fw.png)

**Step 2:** Register an OAuth Application and retrieve the Client Key, Client Secret.

Access the My OPSWAT Central Management. On the right menu, select OAuth Application

![](https://uploads.developerhub.io/prod/97qW/y1hwtl6084c21p7gdjmsssfl41bq0v1os8nzzb898g8tsbvi7nruciky20jwjud1.png)

[Register ](https://www.opswat.com/docs/cm/developer-guidelines/how-to-work-with-apis)an application and retrieve the Client_key and Client_ Secret.

![](https://uploads.developerhub.io/prod/97qW/j7zs9k708ci89oxuy55p36o9hd3mey1bxlebc3aja12zwwsqchlrw5vxgb3yy64p.png)

**Step 3:** Retrieve the Access Token from OAuth 2 Authentication Flow

Use the Client Key and Client Secret from the registered application and call the My OPSWAT Central Management OAuth API to obtain an access token. This token will be used for authenticating subsequent API requests.

```json
curl -X POST 'https://product.my.us.opswat.com/o/oauth2/token' -d 'client_id={{Client ID}}&client_secret={{Client Secret}}&grant_type=client_credentials'
```

**Step 4:** Retrieve the connection ID from MetaDefender Core.

Establish a Direct Instance Management connection from My OPSWAT Central Management to the MetaDefender CORE instance.

Request sample:

```json
curl --location 'https://product.my.us.opswat.com/fusion/console/services/connection/request/mdcore' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{access_token}}' \
--data '{
    "deploymentId": "{{Product_Deployment_Id}",
    "Purpose": "Direct Instance Management"
}'
```

Response example:

```json
{
    "connId": "63BdkJatrysSo4w4tGVjp8ShAtTFJgQfufwstdEG48k4tE6C9wDeLmCR46Ak1C73MkPsL4HAx6WoFixHXzLom5cCQnyRm56JngHK",
    "status": "REQUESTING"
}
```

After creating the connection ID, the status will change from REQUESTING to CONNECTED. The API will work only if the connection status is CONNECTED. Use the below API to check if the connection is successfully established.

Request example

```json
curl --location 'https://product.my.us.opswat.com/fusion/console/services/connection/63BdkJatrysSo4w4tGVjp8ShAtTFJgQfufwstdEG48k4tE6C9wDeLmCR46Ak1C73MkPsL4HAx6WoFixHXzLom5cCQnyRm56JngHK' \
--header 'Authorization: Bearer {{Auth_Token}}'
```

Response example

```json
{
    "connId": "63BdkJatrysSo4w4tGVjp8ShAtTFJgQfufwstdEG48k4tE6C9wDeLmCR46Ak1C73MkPsL4HAx6WoFixHXzLom5cCQnyRm56JngHK",
    "status": "CONNECTED"
}
```

**Step 5:** Re-route API request from MetaDefender Core to My OPSWAT Central Management API:

1. URL: "[https://product.my.us.opswat.com/fusion/console/services/connection/{](https://product.my.us.opswat.com/fusion/console/services/connection/%7B_**connectionID**_%7D%22)[***connectionID***](https://product.my.us.opswat.com/fusion/console/services/connection/%7B_**connectionID**_%7D%22)[}"](https://product.my.us.opswat.com/fusion/console/services/connection/%7B_**connectionID**_%7D%22)
   1. connnectionID: obtain from step 4
2. Method: POST
3. Add the following headers to reflect the MetaDefender Core APIs
   1. ACCESS_TOKEN: obtain from step 3
   2. X-App-Method: obtain from MetaDefender Core API documentation
   3. X-App-URL: obtain from MetaDefender Core API documentation
   4. data: obtain from MetaDefender Core API documentation

```javascript
curl -X POST --location 'https://product.my.us.opswat.com/fusion/console/services/connection/{{CONNECTION_ID}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
--header 'X-App-Method: {{...}}' \
--header 'X-App-URL: {{...}}' \
--data '{{...}}'
```

**Example:** How to re-route **' List all users '**  from MetaDefender Core to My OPSWAT Central Management

1. Get info from MDCore API - [userlist](https://www.opswat.com/docs/mdcore/metadefender-core#userlist)

In this api, need to use method '**GET**' and URL '/**admin/user**'

![](https://uploads.developerhub.io/prod/97qW/0oub2j7vvklkyx73on64li2q3xgw5mjy2bywf494aypn9didmj9qq05v8wug7aju.png)

2. Convert MD Core API to Central Management API as below

API Request

```javascript
curl -X POST --location 'https://product.my.us.opswat.com/fusion/console/services/connection/{{CONNECTION_ID}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
--header 'X-App-Method: GET' \
--header 'X-App-URL: /admin/user'
```

API Response

```json
[{
		"api_key": "12345678901234567890123456789012",
		"directory_id": 1,
		"display_name": "Administrator",
		"email": "trung.dang@opswat.com",
		"id": 2,
		"last_seen_ip": "::1",
		"last_seen_timestamp": 1753717373374,
		"name": "Administrator",
		"rights": {
			"agents": [
				"read",
				"write"
			],
			"banner": [
				"read",
				"write"
			],
			"cert": [
				"read",
				"write"
			],
			"config_file_sync": [
				"read",
				"write"
			],
			"config_webhook": [
				"read",
				"write"
			],
			"configlog": [
				"read",
				"write"
			],
			"download": [
				"anyone"
			],
			"downloadfrom": [
				"read",
				"write"
			],
			"emailnotification": [
				"read",
				"write"
			],
			"engines": [
				"read"
			],
			"engines_update": [
				"read",
				"write"
			],
			"external": [
				"read"
			],
			"fetch": [
				"anyone"
			],
			"healthcheck": [
				"read"
			],
			"license": [
				"read",
				"write"
			],
			"logger": [
				"read",
				"write"
			],
			"maintain": [
				"read",
				"write"
			],
			"passwordstorage": [
				"read",
				"write"
			],
			"quarantine": [
				"read",
				"write"
			],
			"reporting": [
				"read",
				"write"
			],
			"requestrate": [
				"read",
				"write"
			],
			"retention": [
				"read"
			],
			"rule": [
				"read"
			],
			"scan": [
				"read",
				"write"
			],
			"scanlog": [
				"read",
				"write"
			],
			"skip": [
				"read",
				"write"
			],
			"statistics": [
				"read",
				"write"
			],
			"update": [
				"read"
			],
			"updatelog": [
				"read",
				"write"
			],
			"users": [
				"read",
				"write"
			],
			"webhook_auth": [
				"read"
			],
			"workflow": [
				"read"
			],
			"zone": [
				"read"
			]
		},
		"roles": [
			"1"
		],
		"ui_settings": {
			"wf_order": [
				"process_info",
				"archive",
				"compression",
				"filetype_analysis",
				"scan",
				"external_scanner",
				"ds",
				"dlp",
				"filescanio",
				"insightsti",
				"sbom",
				"external_action",
				"mddotcom",
				"vul",
				"blacklist",
				"whitelist",
				"reputation",
				"coo",
				"yara"
			]
		}
	}]
```

### Appendix

**List of APIs supported by Meta Defender CORE**

| APIs | Document | Url | Method | From Version |
| ---- | ---- | ---- | ---- | ---- |
| Create user | [https://www.opswat.com/docs/mdcore/metadefender-core#usercreate](https://www.opswat.com/docs/mdcore/metadefender-core#usercreate) | /admin/user | POST | 5.15.0 |
| List all users | [https://www.opswat.com/docs/mdcore/metadefender-core#userlist](https://www.opswat.com/docs/mdcore/metadefender-core#userlist) | /admin/user | GET | 5.15.0 |
| Delete a user | [https://www.opswat.com/docs/mdcore/metadefender-core#userdelete](https://www.opswat.com/docs/mdcore/metadefender-core#userdelete) | /admin/user/{user_id} | DELETE | 5.15.0 |
| Change user's API key | [https://www.opswat.com/docs/mdcore/metadefender-core#changeuserapikey](https://www.opswat.com/docs/mdcore/metadefender-core#changeuserapikey) | /admin/user/(\d+)/apikey | PUT | 5.15.0 |
| Change Password for local user | [https://www.opswat.com/docs/mdcore/metadefender-core#userchangepass](https://www.opswat.com/docs/mdcore/metadefender-core#userchangepass) | /user/changepassword | POST | 5.15.0 |
| List all roles |  | /admin/role | GET | 5.15.0 |
| List all user directories |  | /admin/userdirectory | GET | 5.15.0 |

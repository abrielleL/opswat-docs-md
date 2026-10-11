<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-do-i-setup-hot-swap-backup-configuration-between-metadefende -->

# How do I setup Hot Swap Backup Configuration between MetaDefender Core instances?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Online procedure**

- Make sure the primary MetaDefender Core deployment is activated
- Gather the deployment ID and Activation key from the primary MetaDefender Core deployment
- Navigate to the secondary MetaDefender Core instance and take the following steps

  - Select the Register as back-up instance option on the back-up MetaDefender Core machine

- - Add the necessary variables from the primary MetaDefender Core deployment and “register” (Primary Core deployment ID and Activation key)

Once the steps are completed, we can observe the successful result on the back-up MetaDefender Core console.

**Api call (online environment)**

In order to successfully set up hot swap backup configuration between 2 or more MetaDefender Core deployments via API calls the following steps need to be followed:

- Make sure the primary MetaDefender Core deployment is activated
- Gather the deployment ID and Activation key from the primary MetaDefender Core deployment
- Use the API call listed below with any preferred solution.

BashCopycurl --request POST \ --url '__http://localhost:8008/admin/license/backup' \ --header 'Content-Type: application/octet-stream' \ --header 'apikey: {apikey}' \ --header 'active-deployment-id: {active-deployment-id}' \ --header 'activation-key: {activation-key}' \ --data-binary '{ "schema": "{string}" }'

A Postman example is highlighted below. Make sure the following information is available before the API call is send:

- API Key from the backup MetaDefender Core server
- Activation key
- Primary MD Core instance deployment ID

Once the steps are completed, we can observe the successful result on the back-up MetaDefender Core console.

**Api call (offline environment)**

In order to successfully set up hot swap backup configuration between 2 or more MetaDefender Core deployments via API calls the following steps need to be followed:

- Make sure the primary MetaDefender Core deployment is activated
- Gather the deployment ID, Activation key, and the offline yml activation file from the primary MetaDefender Core deployment
- Use the API call listed below with any preferred solution.

BashCopycurl --request POST \ --url '__http://localhost:8008/admin/license/backup' \ --header 'Content-Type: application/octet-stream' \ --header 'apikey: {apikey}' \ --header 'active-deployment-id: {active-deployment-id}' \ --header 'activation-key: {activation-key}' \ --data-binary '{ "schema": "{string}" }'

A Postman example is highlighted below. Make sure the following information is available before the API call is send:

- API Key from the backup MetaDefender Core server
- Activation key
- Primary MetaDefender Core instance deployment ID
- .yml activation file from the Primary MetaDefender Core instance

- Use that yml file content in body content of the REST API

Once the steps are completed, we can observe the successful result on the back-up MetaDefender Core console.

Support:

If you encounter any issues during the activation process or require further assistance, please contact OPSWAT support via My OPSWAT at: <https://my.opswat.com/home>

Our support team will be able to provide you with the necessary guidance and resolution for any license-related concerns.

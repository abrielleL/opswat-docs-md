<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/retrieving-username-using-an-api-key -->

# Retrieving Username Using an API Key

If the profile username has been lost, it may still be recovered using a valid **admin API key**, which can be used to send a **GET** Request to the **/admin/user** endpoint to list all the available users and identify the users

Retrieve the list of users by sending a **GET request** to the `/admin/user` API endpoint.

[**GET - List all users**](https://www.opswat.com/docs/mdcore/metadefender-core#userlist)

**Example request:**

curl --get \
--url 'http://localhost:8008/admin/user' \
--header 'apikey: {apikey}'

From the response, identify the user associated with the provided API key and retrieve the corresponding **name**.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

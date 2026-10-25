<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/knowledge-base/how-to-increase-session-timeout-via-api-call- -->

# How to increase session timeout via API call?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

To increase the session timeout on the EGS console via API call you will need the following resources from the EGS instance:

- An API key generated from the EGS console.

- A valid URL from the EGS instance we are trying to make this change.

Once we have the two items mentioned above we will need to use the following API call to make the change to the session timeout value:

BashCopycurl --request PUT \ --url 'http://localhost:8058/admin/config/session' \ --header 'Content-Type: application/json' \ --header 'apikey: {apikey}' \ --data '{ "absoluteSessionTimeout": 0, "allowCrossIpSessions": true, "allowDuplicateSession": true, "sessionTimeout": 300000 }'

The value for the highlighted images from above is set to milliseconds.

Having the “0” value as can be seen in the image above will result in the timeout setting to be disabled.

Additionally, modifying the **"allowCrossIpSessions": true**, and **"allowDuplicateSession": true**, will allow users to:

- "allowCrossIpSessions": true - Enable sessions from multiple IP addresses for users
- "allowDuplicateSession": true - Enable duplicate sessions for users

If the values are set to false for any of the entries the functionality will no longer be available.

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support-services).

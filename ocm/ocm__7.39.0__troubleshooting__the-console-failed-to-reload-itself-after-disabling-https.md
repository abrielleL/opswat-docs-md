<!-- source: https://www.opswat.com/docs/ocm/7.39.0/troubleshooting/the-console-failed-to-reload-itself-after-disabling-https -->

# The console failed to reload after disabling HTTPS in Secure Connection settings

| Type | Detail |
| --- | --- |
| Problem | After disabling HTTPS mode in [Secure Connection](/docs/ocm/7.39.0/configuration/enabling-https) settings, the console failed to load with an error related to a secure connection. |
| Cause | The [Server URL](/docs/ocm/7.39.0/configuration/setting-up-domain) has not updated to **http://**. |
| Troubleshooting | Can access the management console with **http://** prefix |
| Solution | Manually change the Server URL prefix to **http://.** |

After disabling HTTPS mode in [Secure Connection](/docs/ocm/7.39.0/configuration/enabling-https) settings without manually updating Server URL to HTTP, the console failed to reload .

For instance, you may see the error "This site can't provide a secure connection" on Google Chrome.

One possible cause is that upon disabling HTTPS mode, the Server URL's protocol prefix was not updated to **http://** manually**.** By default, the console will be reloaded with the configured Server URL. In other words, it will be reloaded with https and as a result, the OCM instance cannot provide a secure connection, the web browser will encounter an error.

You need to manually change the console URL to http on your web browser to able to access the console and follow the document [here](/docs/ocm/7.39.0/configuration/setting-up-domain) to update the Server URL to http.

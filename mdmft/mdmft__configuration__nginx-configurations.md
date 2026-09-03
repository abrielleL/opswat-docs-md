<!-- source: https://www.opswat.com/docs/mdmft/configuration/nginx-configurations -->

# Nginx configurations

Summarize Page    Connect to Cursor Connect to VS Code
## [Restrictions](https://www.opswat.com/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#restrictions)

**Only allow access to our domain only**

Only requests to example.in, www.example.in, or images.example.in are allowed. All other requests are dropped silently, reducing exposure to unauthorized traffic and preventing domain spoofing.

if ($host !~ ^(example.in|www.example.in|images.example.in)$ ) {
return 444;
}

**Deny certain user-agents**

Requests from specified user-agents are blocked, reducing abuse from automated tools and bots.

## Block download agents ##
if ($http_user_agent ~* LWP::Simple|BBBike|wget) {
return 403;
}
##
## Block robots ##
if ($http_user_agent ~* msnbot|scrapbot) {
return 403;
}
##

**Block referral spam**

Requests with referrers containing these keywords are blocked, reducing referral spam and abuse. Only direct access or requests from legitimate sources are allowed.

## Deny certain Referers ###
if ( $http_referer ~* (babes|forsale|girl|jewelry|love|nudit|organic|poker|porn|sex|teen) ) {
return 403;
}
##

**Block particular APIs**

Requests to /admin/config/session are blocked, preventing unauthorized access to this API.

## Block particular api ###
location ~ "^/admin/config/session$" {
return 403;
}
##

**How to configure**

**Step 1: Create a .conf file under** ***<Installation Directory>*****\WebServer\conf**

Here is sample .conf file. Choose what meets to your scenario and update .conf file

if ($host !~ ^(example.in|www.example.in|images.example.in)$ ) {
return 444;
}
if ($http_user_agent ~* LWP::Simple|BBBike|wget) {
return 403;
}
if ($http_user_agent ~* msnbot|scrapbot) {
return 403;
}
if ( $http_referer ~* (babes|forsale|girl|jewelry|love|nudit|organic|poker|porn|sex|teen) ) {
return 403;
}

**Step 2: A restart of the "MetaDefender Managed File Transfer™" services are required.**

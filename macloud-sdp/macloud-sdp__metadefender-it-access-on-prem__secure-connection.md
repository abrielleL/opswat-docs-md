<!-- source: https://www.opswat.com/docs/macloud-sdp/metadefender-it-access-on-prem/secure-connection -->

# How to setup a secure connection

By default, the communication between a clients and an MetaDefender IT Access OnPrem server is not encrypted. If HTTPS is enabled, the server can enforce secure connections between clients and the server on SSL channels. This section describes how to enable SSL for MetaDefender IT Acces OnPrem

#### [Enabling HTTPS](/docs/macloud-sdp/metadefender-it-access-on-prem/secure-connection#enabling-https)

MetaDefender IT Access OnPrem supports accessing admin console and API via HTTPS. This feature is not enabled by default.

There are two ways to enable the feature:

- Using my own domain (custom domain)
- Using a provided subdomain for on-prem deployment (Free custom Subdomain *.maop.site)

#### [Using my own domain (Custom domain)](/docs/macloud-sdp/metadefender-it-access-on-prem/secure-connection#using-my-own-domain-custom-domain)

- The administrator needs to enter their own domain and upload SSL/TLS certificate.

Warning

you should use a valid domain and certificate. If you’re using a self-sign certificate, you must install the certificate on any device clients that connect to your own domain

#### [Using a provided subdomain for on-prem deployment (Free Custom Subdomain *.maop.site)](/docs/macloud-sdp/metadefender-it-access-on-prem/secure-connection#using-a-provided-subdomain-for-on-prem-deployment-free-custom-subdomain-maopsite)

- MetaDefender IT Access OnPrem will provide a subdomain such as <customer company>.maop.site
- MetaDefender IT Access OnPrem will use a wildcard cert to issue a cert for the subdomain
- By using DNS API, MetaDefender IT Access will associate the on-prem IP to <customer company>.maop.site
- MetaDefender IT Access OnPrem will use the wildcard cert for *.maop.site

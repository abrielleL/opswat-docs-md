<!-- source: https://www.opswat.com/docs/mdcore/configuration/nginx-configurations -->

# NGINX Configuration

Hardening guideline for Nginx web server are recommended by the vendor, and optional steps to MetaDefender Core product. Please only follow them when applicable.

Those guidelines are supported since MetaDefender Core version 4.19.0 or above.

## [Restrictions](/docs/mdcore/configuration/nginx-configurations#restrictions)

### [Only allow access to our domain only](/docs/mdcore/configuration/nginx-configurations#only-allow-access-to-our-domain-only)

if ($host !~ ^(metadefendercore.in|www.metadefendercore.in|images.metadefendercore.in)$ ) {
return 444;
}
### [Deny certain user-agents](/docs/mdcore/configuration/nginx-configurations#deny-certain-user-agents)

Blocking user-agents i.e. scanners, bots, and spammers who may be abusing your server.

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
### [Block referral spam](/docs/mdcore/configuration/nginx-configurations#block-referral-spam)

Only direct access is allowed

## Deny certain Referers ###
if ( $http_referer ~* (babes|forsale|girl|jewelry|love|nudit|organic|poker|porn|sex|teen) ) {
return 403;
}
##
### [Block particular APIs](/docs/mdcore/configuration/nginx-configurations#block-particular-apis)

## Block particular api ###
location ~ "^/admin/config/session$" {
return 403;
}
##
### [How to configure](/docs/mdcore/configuration/nginx-configurations#how-to-configure)

Step 1: Create a .conf file (create “built-in” folder if not existed)

- On Windows, under ***<Installation Directory>\nginx\built-in***
- On Linux, under **/etc/ometascan/nginx.d/built-in/**

Here is sample .conf file. Choose what meets to your scenario and update .conf file

if ($host !~ ^(metadefendercore.in|www.metadefendercore.in|images.metadefendercore.in)$ ) {
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

Step 2: A restart of the “OPSWAT MetaDefender Core” service is required.

### [OSCP - Online Certificate Status Protocol](/docs/mdcore/configuration/nginx-configurations#oscp---online-certificate-status-protocol)

1.) Modify “ssl.conf” file (create new if not existed)

- On Windows, under ***<Installation Directory>\nginx***
- On Linux, under **/etc/ometascan/nginx.d/**

Modify ssl.conf file with following recommended settings

# Enable OCSP stapling, optimize session cache
ssl_ecdh_curve secp384r1;
ssl_session_timeout 1d;
ssl_session_cache shared:SSL:10m;
ssl_session_tickets off;
ssl_stapling on;
ssl_stapling_verify on;
 
# verify chain of trust of OCSP response using Root CA and Intermediate certs
ssl_trusted_certificate /path/to/root_CA_cert_plus_intermediates;
 
# replace with the IP address of your resolver
resolver 127.0.0.1;

2.) A restart of the “OPSWAT MetaDefender Core” service is required.

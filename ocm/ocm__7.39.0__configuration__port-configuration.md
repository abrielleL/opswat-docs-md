<!-- source: https://www.opswat.com/docs/ocm/7.39.0/configuration/port-configuration -->

# Port Configuration

For more detail on the ports by OPSWAT Central Management, please refer to [Ports used](/docs/ocm/7.39.0/installation/recommended-system-requirements#ports-used).

Currently, only the web management interface port and the load balancer status port are configurable. Please follow the below guidelines to modify them.

## [On Windows:](/docs/ocm/7.39.0/configuration/port-configuration#on-windows)

1. Locate the file ProgramData/OPSWAT/Central/config.properties.
2. You can modify the web management interface port (**nginx_port**, default 9000) and the load balancer status port (**up_port**, default 9026).

tomcat_port=9009
mongo_port=27017
memcached_port=9005
nginx_port=9000
up_port=9026

3. For the interface port:

   1. Locate the file Program Files/OPSWAT/Central/nginx/conf/serverSettings.conf
   2. Change listen to the same value as nginx_port as set in step 2.

listen 9000;
listen [::]:9000;

4. For the status port:

   1. Locate the file Program Files/OPSWAT/Central/nginx/conf/up.conf
   2. Change the port number after **listen** to the same value as up_port as set in step 2.

listen 9026;

5. Restart OPSWAT Central Management via the tray icon.

## [On Red Hat Enterprise Linux/Ubuntu:](/docs/ocm/7.39.0/configuration/port-configuration#on-red-hat-enterprise-linuxubuntu)

1. Locate the file /usr/lib/ocm/set-port.sh
2. You can modify the web management interface port (**nginx_port**, default 9000) and the load balancer status port (**up_port**, default 9026).

tomcat_port=9009
mongo_port=27017
memcached_port=9005
nginx_port=9980
up_port=9026

3. For the interface port:

   1. Locate the file /opt/ocm/nginx/conf/serverSettings.conf
   2. Change **listen** to the same value as nginx_port as set in step 2.

listen 9000;
listen [::]:9000;

4. For the status port:

   1. Locate the file/opt/ocm/nginx/conf/up.conf
   2. Change the port number after **listen** to the same value as up_port as set in step 2.

listen 9026;

5. Restart OPSWAT Central Management via the command systemctl restart ocm.

Warning

After changing the web management console port, you will also need to update the Server URL setting to reflect the new address. Please refer to [Server URL](/docs/ocm/7.39.0/configuration/setting-up-domain).

Devices managed by OPSWAT Central Management will require MetaDefender Endpoint's reinstallation upon an address change.

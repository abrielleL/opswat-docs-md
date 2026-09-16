<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/origin-client-source-identification -->

# Origin Client Source Identification

By default, when triggering scan from client through a load balancer or proxy server, MetaDefender Core’s Nginx web server will not identify the original client source (but the load balancer or proxy server’s address instead).

In order to force Nginx web server to trace back the origin client source:

1.) Create a “extra.conf” file

- On Windows, under ***<Installation Directory>\nginx***
- On Linux, under **/etc/ometascan/nginx.d/**

set_real_ip_from 192.168.1.1;
real_ip_header X-Forwarded-For;
real_ip_recursive on;

Make sure to change “192.168.1.1” to your actual load balancer or proxy server address.

In cases involving multiple load balancers, you can specify all the load balancer IP addresses in the `set_real_ip_from` directive.

set_real_ip_from 192.168.1.1;
set_real_ip_from 192.168.1.2;
set_real_ip_from 192.168.1.3;
real_ip_header X-Forwarded-For;
real_ip_recursive on;

If you use a virtual IP (VIP) for a load balancer cluster, you can specify that VIP instead.

set_real_ip_from <VIP_Address>;
real_ip_header X-Forwarded-For;
real_ip_recursive on;

2.) A restart of the “OPSWAT Metadefender Core” service is required.

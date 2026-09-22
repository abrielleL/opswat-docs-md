<!-- source: https://www.opswat.com/docs/cm/deployment/how-to-setup-a-secure-connection -->

# How to Setup a Secure Connection

By default, the communication between a clients and an My OPSWAT Central Management OnPrem server is not encrypted. If HTTPS is enabled, the server can enforce secure connections between clients and the server on SSL channels. This section describes how to enable SSL for MetaDefender IT Acces OnPrem

#### Enabling HTTPS

My OPSWAT Central Management OnPrem supports accessing admin console and API via HTTPS. This feature is not enabled by default.

There are two ways to enable the feature:

- Using my own domain (custom domain)
- Using a provided subdomain for on-prem deployment (Free custom Subdomain *.maop.site)

![](https://uploads.developerhub.io/prod/97qW/vwdzgeow8owppi4nd46pwkqox6vjxgz4blay135ypr0wtmwlwd0d62vr0gz1gotv.png)

#### Using my own domain (Custom domain)

- The administrator needs to enter their own domain and upload SSL/TLS certificate.

> **Warning**
>
> you should use a valid domain and certificate. If you’re using a self-sign certificate, you must install the certificate on any device clients that connect to your own domain

![](https://uploads.developerhub.io/prod/97qW/eijom811abypq1w7mgx17rccg3mayg6ixjeo99sl1gryje2ijfonmhtvu2sb681m.png)

#### Using a provided subdomain for on-prem deployment (Free Custom Subdomain *.maop.site)

- My OPSWAT Central Management OnPrem will provide a subdomain such as <customer company>.maop.site
- My OPSWAT Central Management OnPrem will use a wildcard cert to issue a cert for the subdomain
- By using DNS API, My OPSWAT Central Management will associate the on-prem IP to <customer company>.maop.site
- My OPSWAT Central Management OnPrem will use the wildcard cert for *.maop.site

![](https://uploads.developerhub.io/prod/97qW/vvhxgh8xiprebzebzxqgwwxuwplopuuimvn8x6agdsagllhx7rweqra4o9r8zug6.png)

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)

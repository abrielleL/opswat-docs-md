<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/f5-big-ip-ssl-configuration -->

# F5 BIG IP SSL configuration

To scan data transmitted using SSL connection you have to take similar steps as listed in [F5 BIG IP LTM](/integrations/f5-big-ip-ltm).

The only difference is that you should setup a HTTPS pool and virtual server instead of plain HTTP.

Please check the following links to be able to setup HTTPS connection handling:

- [Managing client-side HTTPS traffic using a self-signed certificate](https://techdocs.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/ltm-implementations-11-5-1/9.html)
- [Managing client and server HTTPS traffic using a self-signed certificate](https://techdocs.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/ltm-implementations-11-5-1/10.html)
- [Managing client-side HTTPS traffic using a CA-signed certificate](https://techdocs.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/ltm-implementations-11-5-1/12.html)

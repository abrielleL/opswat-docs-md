<!-- source: https://www.opswat.com/docs/mdemail/knowledge-base/can-i-configure-two-ssl-certificates-for-one-inbound-outbound-po -->

# Can I configure two SSL certificates for one inbound/outbound port in Email Gateway Security?

**Configuring two SSL certificates on a single port in EGS is not possible.**

EGS is designed to use one SSL certificate per port to maintain clear and secure communication channels. This ensures that the SSL handshake and encryption process is consistent for all connections on that port.

If your deployment requires using multiple SSL certificates, for example, to serve different domains or security profiles, you can configure separate inbound/outbound ports. Each port can be assigned its own dedicated SSL certificate.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).

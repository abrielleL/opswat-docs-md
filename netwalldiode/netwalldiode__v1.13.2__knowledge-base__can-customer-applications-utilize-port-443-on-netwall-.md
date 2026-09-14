<!-- source: https://www.opswat.com/docs/netwalldiode/v1.13.2/knowledge-base/can-customer-applications-utilize-port-443-on-netwall- -->

# Can Customer Applications Utilize Port 443 on NetWall?

This article applies to all NetWall products with latest versions (USG/BGS v5.12.1, Optical Diode v1.12.1, Transfer Guard v1.8.1/2.3.1)

In earlier NetWall versions, port 443 could not be used for application or stream configuration because it was reserved exclusively by the NetWall system.

Port 443 was dedicated to the Web Console, providing secure HTTPS access to the NetWall management interface. As a result, customers were unable to configure applications or streams that required port 443.

In the latest NetWall releases, port 443 no longer needs to be exclusive to a single service as long as each service is bound to a different IP address.

Instead of requiring the HTTPS management interface to move to a different port, NetWall allows port 443 to be used by different services when each service is configured on a separate IP address.

How It Works

NetWall separates the use of port 443 based on the IP address.

- The NetWall HTTPS Web Console continues to use port 443 on the specific IP address.
- Other applications or TCP stream configurations can also use port 443, provided they are configured with a different IP address. For example, if interface ENO1 has two IP addresses:

20.20.20.20 20.20.20.21

The management Web Console can use 20.20.20.20:443, while a TCP stream can use 20.20.20.21:443.

- Although both IP addresses may exist on the same physical interface, there is no port conflict because the services are bound to different IP addresses.

In summary, port 443 does not necessarily need to be changed to another port for the Web Console. NetWall can allow the same port to be used by multiple services as long as each service is bound to a separate IP address.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

MetaDefender

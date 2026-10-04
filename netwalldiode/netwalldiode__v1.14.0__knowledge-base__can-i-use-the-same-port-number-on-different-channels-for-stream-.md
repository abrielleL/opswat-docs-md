<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/knowledge-base/can-i-use-the-same-port-number-on-different-channels-for-stream- -->

# Can I use the same port number on different channels for stream connections on MetaDefender Optical Diode?

This article applies to all Metadefender Optical Diode version 1.11.0 and higher.

## [Background](/docs/netwalldiode/v1.14.0/knowledge-base/can-i-use-the-same-port-number-on-different-channels-for-stream-#background)

Customers may have applications that can communicate over one specific port. When adding this port to the stream configuration, no other stream was able to utilize the same port number even on a different channel.

## [Solution:](/docs/netwalldiode/v1.14.0/knowledge-base/can-i-use-the-same-port-number-on-different-channels-for-stream-#solution)

Starting with MetaDefender Optical Diode version 1.11.0, support for multiple VLANs is now available and a specific port per channel is no longer a limitation. Customers can now make use of “Bind IP Address” feature, that will allow the bind of a specific IP address to a port per channel in the stream configuration. This will allow to use the same port number on different stream connections.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/support).

MetaDefender

<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/troubleshooting/why-will-sdp-sometimes-refuse-to-connect-at-random-intervals- -->

# Why will SDP sometimes refuse to connect at random intervals?

**Issue**

Users may experience intermittent failures when attempting to connect with OPSWAT MetaDefender Endpoint SDP. These failures may appear to occur at random intervals without any apparent trigger.

**Cause**

This issue is typically caused by a conflict between MetaDefender Endpoint SDP and other VPN software installed on the same machine.

Since SDP operates as a VPN-like functionality, it relies on similar networking components and drivers. If another VPN product is running or has recently initialized, it may reserve or alter networking resources (such as virtual adapters or routing tables) in a way that interferes with SDP’s ability to establish its own secure connection.

**Resolution**

To avoid conflicts and ensure stable operation of MetaDefender Endpoint SDP:

1. **Do not run multiple VPN applications simultaneously.** Ensure that any other VPN clients are fully closed or disabled before launching the SDP client.
2. **Restart SDP after closing other VPNs.** If another VPN is active, fully close it, then restart the SDP client to reinitialize its network stack.
3. **Consider uninstalling conflicting VPNs.** If regular use of MetaDefender Endpoint SDP is required, and other VPN applications are not essential, consider removing them to prevent ongoing conflicts.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

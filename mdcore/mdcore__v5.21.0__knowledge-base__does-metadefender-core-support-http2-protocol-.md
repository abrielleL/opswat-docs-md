<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/does-metadefender-core-support-http2-protocol- -->

# Does MetaDefender Core support HTTP2 Protocol?

**Description**

This article clarifies whether MetaDefender Core supports the HTTP/2 protocol for client-server communications. It is intended for customers and integrators who are evaluating network, performance, or compatibility requirements when deploying MetaDefender Core behind load balancers, reverse proxies, or modern web servers.

**Response**

No, MetaDefender Core does not support the HTTP/2 protocol.

MetaDefender Core currently supports HTTP/1.0 and HTTP/1.1 only for all API and web-based communications. Native HTTP/2 connections are not supported by the MetaDefender Core application itself.

**Technical Details**

- MetaDefender Core’s embedded web services and APIs are designed to operate over HTTP/1.x.
- Features specific to HTTP/2—such as multiplexed streams, header compression (HPACK), and binary framing—are not implemented at the application level.
- When deployed behind a reverse proxy or load balancer (e.g., NGINX, HAProxy, F5), HTTP/2 may be used externally (client → proxy), but traffic must be downgraded to HTTP/1.1 between the proxy and MetaDefender Core.

**Deployment Implications**

- This limitation does not affect standard API functionality, performance, or security in supported configurations.
- If HTTP/2 is required for client-facing traffic, it is recommended to terminate HTTP/2 at a reverse proxy and forward requests to MetaDefender Core using HTTP/1.1.
- This approach is fully compatible with common enterprise architectures and does not require changes to MetaDefender Core.

**Summary**

- HTTP/2 supported: ❌ No
- HTTP versions supported: ✅ HTTP/1.0, HTTP/1.1
- Recommended workaround: Use HTTP/2 termination at a reverse proxy, forward to MetaDefender Core over HTTP/1.1

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

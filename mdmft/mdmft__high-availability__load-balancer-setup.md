<!-- source: https://www.opswat.com/docs/mdmft/high-availability/load-balancer-setup -->

# Load Balancer Setup

Summarize Page    Connect to Cursor Connect to VS Code

The purpose of deploying multiple MetaDefender MFT HA Controller™ instances is to place them behind a **load balancer**. The load balancer distributes incoming user requests across all available HA Controller peers. The load balancer can be any third-party solution.

## [MetaDefender MFT HA Controller™ health check](/docs/mdmft/high-availability/load-balancer-setup#ha_controller_product_name_short-health-check)

Each MetaDefender MFT HA Controller™ exposes a dedicated health endpoint at:

`http://<your-ha-controller-address>:<port>/ha-controller/health`

This endpoint allows the Load Balancer to periodically verify the status of each controller. You can configure the load balancer to poll this endpoint at regular intervals, and only forward user requests to instances that respond successfully to the health check.

| Condition | HTTP Status | Meaning |
| --- | --- | --- |
| Application is healthy | 200 OK | The service is functioning normally and can handle traffic. |
| Application is unhealthy | 503 Service Unavailable | The service isn’t ready to handle traffic and should be treated as unhealthy by load balancers and orchestrators. |

## [Load Balancer modes](/docs/mdmft/high-availability/load-balancer-setup#load-balancer-modes)

The Load Balancer can operate in **TCP mode (Layer 4)** or **HTTP mode (Layer 7)**. Both modes can distribute traffic to multiple MetaDefender MFT HA Controller™ instances.

## [HTTP Mode](/docs/mdmft/high-availability/load-balancer-setup#http-mode)

When using HTTP mode on the load balancer, it should be configured to append the `X-Forwarded-For` (XFF) header so that the original client IP is included with each forwarded request.

Additionally, the MetaDefender® MFT application must be configured to trust the load balancer’s IP address as a forwarder, this means adding the load balancer and each MetaDefender MFT HA Controller™’s IP to the list of trusted forwarders so that the `X-Forwarded-For` header is accepted and used to determine the client’s real address.

### [Trusted Forwarder configuration](/docs/mdmft/high-availability/load-balancer-setup#trusted-forwarder-configuration)

Below is an example Trusted Forwarder setup with a load balancer in front of three MetaDefender MFT HA Controller™ instances.

You can find more information about Trusted Forwarder configuration [here](/docs/mdmft/configuration/trusted-forwarder).

## [Example](/docs/mdmft/high-availability/load-balancer-setup#example)

Below is an example [HAProxy](https://www.haproxy.com/) configuration showing how to set up HAProxy as an HTTP load balancer in front of your MetaDefender MFT HA Controller™ peers. In this example, the Load Balancer performs health checks against a custom health endpoint and uses the **round-robin** algorithm to distribute requests among the MetaDefender MFT HA Controller™ instances. The three peers are listed in the `web_backends` section with health checks enabled.

You can find more details about HAProxy configuration in the official [HAProxy documentation](https://www.haproxy.com/documentation/haproxy-configuration-manual/latest/#2)

HTTPTCPCopyglobal
log stdout format raw local0
maxconn 4096
defaults
mode http
timeout connect 5s
timeout client 50s
timeout server 50s
option httplog
frontend http_front
bind *:8080 ssl crt /etc/haproxy/certs/cert.pem
option forwardfor
default_backend web_backends
backend web_backends
mode http
option httpchk GET /ha-controller/health
http-check expect status 200
default-server inter 2s fall 1 rise 1
balance roundrobin
server web1 192.168.0.1:8100 check
server web2 192.168.0.2:8100 check
server web3 192.168.0.3:8100 checkglobal
log stdout format raw local0
maxconn 4096
defaults
mode tcp
timeout connect 5s
timeout client 50s
timeout server 50s
option tcplog
frontend http_front
bind *:8080 ssl crt /etc/haproxy/certs/cert.pem
default_backend web_backends
backend web_backends
mode tcp
balance roundrobin
server web1 192.168.0.1:8100 check
server web2 192.168.0.2:8100 check
server web3 192.168.0.3:8100 check

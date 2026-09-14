<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/high-availability/two-site-load-balancer-setup -->

# Load Balancer Setup

Summarize Page    Connect to Cursor Connect to VS Code
### [Health Endpoint](/docs/mdmft/v3.11.4/high-availability/two-site-load-balancer-setup#health-endpoint)

The MetaDefender® MFT service exposes a dedicated health check endpoint designed for load balancer integration. Your load balancer can periodically poll this endpoint and use the HTTP response code to decide whether to route traffic to each node.

| Property | Value |
| --- | --- |
| URL | `http://your-mft-server:8010/node_manager/health/ready` |
| Method | GET |
| Authentication | None required (publicly accessible) |

### [Routing Logic](/docs/mdmft/v3.11.4/high-availability/two-site-load-balancer-setup#routing-logic)

- **Healthy**: Any `2xx` response means the node is ready to handle traffic.
- **Unhealthy**: Any `5xx` response or request timeout means the node is not ready — traffic should be routed to other healthy nodes.

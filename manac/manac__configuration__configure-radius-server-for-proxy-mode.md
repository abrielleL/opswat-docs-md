<!-- source: https://www.opswat.com/docs/manac/configuration/configure-radius-server-for-proxy-mode -->

# Configure RADIUS Server for Proxy Mode

## [Configure Home Server Proxy Rules](/docs/manac/configuration/configure-radius-server-for-proxy-mode#configure-home-server-proxy-rules)

## [Step-by-step guide](/docs/manac/configuration/configure-radius-server-for-proxy-mode#step-by-step-guide)

Home Server Proxy rules are only used in situations where more than one Home Server pool is configured. If there is only Home Server pool, there is no need to configure any proxy rules. To configure Proxy rules, click on the “Pool Proxy Rules” tab, and select the “Default” pool. Any traffic that does not match a proxy rule will be forwarded to the “Default” pool. To add a proxy rule click on the “Add Rule” button:

Proxy rules can fully support regular expression and can match one of three criteria:

- **Domain:** Also referred to as realm. This is the domain portion of a username following one of these formats:

  - **DOMAIN**\username
  - username@**domain**
- **NAS IP:** This will match against a specific NAS IP address. A NAS could be a wireless controller, ap or wired switch.
- **Username:** Will match against any portion of username.

A single rule can have multiple conditions. If multiple conditions are specified, note that a RADIUS request must match ALL criteria for the rule to apply. If OR conditions are needed, additional rules must be created. Below is two examples proxy rules.

### [Single Condition:](/docs/manac/configuration/configure-radius-server-for-proxy-mode#single-condition)

### [Multiple Conditions:](/docs/manac/configuration/configure-radius-server-for-proxy-mode#multiple-conditions)

After creating rules, a pool can be chosen for RADIUS requests that match a specific rule. In this example, two rules have been created that forward RADIUS requests to an alternate pool. Any traffic that does not match either of these two rules will be forwarded to the default pool:

## [Related articles](/docs/manac/configuration/configure-radius-server-for-proxy-mode#related-articles)

Error rendering macro 'contentbylabel' : parameters should not be empty

---

## [Configure Home Servers and Pools](/docs/manac/configuration/configure-radius-server-for-proxy-mode#configure-home-servers-and-pools)

## [Step-by-step guide](/docs/manac/configuration/configure-radius-server-for-proxy-mode#step-by-step-guide)

### [Configure Home Servers and Pools](/docs/manac/configuration/configure-radius-server-for-proxy-mode#configure-home-servers-and-pools)

Click on “Home Server” from the left navigation. By default, a single Home Server Pool will be created. If there is only one RADIUS server, or all RADIUS servers are configured the same, there is no need to add additional pools. If there are multiple groups of RADIUS servers, click on “New Pool” to create a pool for each set of RADIUS servers. To add additional Home Servers, click on the green add (+) icon inside the pool.

Each pool can be given a label and can be set be either a “Load Balanced Pool” or a “Failover” pool. A “Load Balanced Pool” will evenly distribute RADIUS requests across all servers in the pool. A “Failover” pool will send all requests to the first server in the list unless it detects that server is no longer responding, in which case, it will failover to the next server in the pool.

Each Home server must be configured individually to communicate with NAC with the following information:

- **Name:** A label to help identify the Home Server at a later time.
- **IP Address:** The IP address of the Home Server.
- **Auth Port:** The port for all RADIUS authentication requests to be sent. This will almost always be the default value.
- **Shared Secret:** A key that is specific to the communication between NAC and the Home Server.

After configuring Home Servers in NAC , a RADIUS client must be configured on each Home Server. On the Home Server side, the shared secret must match the shared secret configured on the NAC side. Below is an example of a single Home Server configuration and a multi-server/multi-pool configuration:

#### [Single Home Server Configuration:](/docs/manac/configuration/configure-radius-server-for-proxy-mode#single-home-server-configuration)

#### [Multi-server/multi-pool Configuration:](/docs/manac/configuration/configure-radius-server-for-proxy-mode#multi-servermulti-pool-configuration)

After completing the home server configuration in both NAC and the Home Server side, each Home server can be tested by selecting the Home Server and choosing “Test Selected” from “Actions” menu.

## [Related articles](/docs/manac/configuration/configure-radius-server-for-proxy-mode#related-articles)

Error rendering macro 'contentbylabel' : parameters should not be empty

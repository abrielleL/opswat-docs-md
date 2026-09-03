<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email- -->

# How to restrict Management Console Access in MetaDefender Email Gateway Security?

This article applies to all MetaDefender Email Gateway Security V5 and 6 releases deployed on Windows systems.

## [Overview](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#overview)

MetaDefender Email Gateway Security (MDES) provides the ability to separate the **web management console** from the **public rescan page** by using different ports and/or network interfaces. This design allows administrators to expose only the services that must be publicly reachable (such as the public *rescan* page) while restricting access to the management console so it is available only from a trusted management network.

By properly configuring these options, you can significantly reduce the attack surface of your MDES deployment and ensure that administrative access is limited to authorized networks.

## [Key Concept](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#key-concept)

- **Management Console**: Intended for administrators only and should be accessible exclusively from a trusted management network.
- **Public Rescan Page**: Can be exposed publicly to allow external users to rescan files or emails, depending on your use case.

MDES supports separating these services by binding them to:

- Different **ports**
- Different **network interfaces (NICs)**

## [Important Limitation](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#important-limitation)

MetaDefender Email Gateway Security **does not support per-subnet allowlists/denylists (whitelist/blacklist)** for management console access in the native UI.

As a result, access control must be enforced using:

- Network interface binding, and/or
- Firewall or network-level rules

## [Configuration Options](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#configuration-options)

### [Option 1: Bind the Management Console to a Management Network Interface (Recommended)](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#option-1-bind-the-management-console-to-a-management-network-interface-recommended)

If your server has **multiple NICs**, you can bind the management console to an internal (management) network interface only, while exposing the public rescan page on a separate interface.

#### [High-Level Steps](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#high-level-steps)

1. Assign:

   - **NIC1** → Internal / Management network
   - **NIC2** → Public or DMZ network
2. Configure the MDES registry settings to bind the REST (management) service to NIC1.
3. Configure the public rescan service and public server address to use NIC2.
4. Allow only trusted network traffic to reach the management interface.

#### [Registry Configuration](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#registry-configuration)

Follow the registry configuration guidance documented here:

- <https://www.opswat.com/docs/mdemail/configuration>

Set the following values:

- `restaddress` = **IP1** (NIC1 – management network)
- `restport` = **8058** (example management console port)
- `public_rescan_port` = **8059** (example public rescan port)

#### [Console Configuration](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#console-configuration)

In the MDES Console:

- Navigate to: **EGS Console > Settings > General > Configuration**
- Set **Public server address** to **IP2** (NIC2 – public network)

#### [Network Controls](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#network-controls)

- Ensure only the trusted management network or subnet can reach **IP1:8058**.
- Do not expose the management interface IP to the public internet.

### [Option 2: Use a Single Network Interface with Firewall Restrictions](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#option-2-use-a-single-network-interface-with-firewall-restrictions)

If your server has **only one NIC**, you can still reduce exposure by separating services by port and enforcing access control using a firewall or network rules.

#### [Steps](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#steps)

1. Bind the management console and public rescan page to **different ports**:

   - `restport` → Management console (for example, 8058)
   - `public_rescan_port` → Public rescan page (for example, 8059)
2. Place firewall or network security rules in front of the server:

   - Allow access to the **management console port** only from trusted IPs or subnets.
   - Allow public access only to the **public rescan port**.

This approach ensures that even though both services share the same interface, administrative access remains restricted.

## [Additional Documentation](/docs/mdemail/6.4.1/knowledge-base/how-to-restrict-management-console-access-in-metadefender-email-#additional-documentation)

For more detailed guidance, refer to the official OPSWAT documentation:

- Restricting Web Management Port: <https://www.opswat.com/docs/mdemail/configuration/hardening#restrict-web-management-port>
- Registry Configuration Reference: <https://www.opswat.com/docs/mdemail/configuration>

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).

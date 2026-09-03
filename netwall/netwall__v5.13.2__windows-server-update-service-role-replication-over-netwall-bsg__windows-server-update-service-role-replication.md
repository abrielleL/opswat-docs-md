<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/windows-server-update-service-role-replication-over-netwall-bsg/windows-server-update-service-role-replication -->

# Windows Server Update Service Role Replication

This document is a guide for implementation of Windows Server Update Services (WSUS) Replication from IT (RED zone) to OT (BLUE zone) using MetaDefender Bilateral Security Gateway.

It assumes the reader is familiar with Windows Server Update Services (WSUS). For more information about WSUS, local configuration tasks, and decisions that are appropriate for you organization, please consult your IT department or read the following article:

<https://learn.microsoft.com/en-us/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus>

There are two distinct modes in which the replicated OT (BLUE) WSUS can work:

- As a “Replica”
- As a Standalone WSUS Server inside OT network.

Both scenarios are covered via the same MetaDefender Bilateral Security Gateway installation procedure. These two logical scenarios are then configured on the OT network WSUS Server. A “Replica” scenario differs from the “Standalone” scenario in only the delegation of who “Approves” the updates. Please consult Microsoft documentation about WSUS for more information.Auto-generated with new documentation.

## [Before you begin](/docs/netwall/v5.13.2/windows-server-update-service-role-replication-over-netwall-bsg/windows-server-update-service-role-replication#before-you-begin)

There are a list of things you will need before you begin:

- You will need to know the IP address/port of the IT WSUS Server.
- You will need to know the IP addresses of the MetaDefender Security Gateway (BLUE) and MetaDefender Security Gateway (RED).
- If you choose to utilize SSL, you will need to do additional steps on both BLUE/RED WSUS servers, to allow for SSL trust to be established.

Note

These pre-conditions are not relevant to MetaDefender Security Gateway configuration, rather, they affect the WSUS services running on both BLUE/RED networks.

This guide assumes WSUS role has been installed on Windows 2019 Server – Standard edition. A replica of the WSUS will be implemented in the BLUE domain, that also assumes WSUS role has been installed on Windows 2019 Server – Standard edition.

## [Example Replication diagram](/docs/netwall/v5.13.2/windows-server-update-service-role-replication-over-netwall-bsg/windows-server-update-service-role-replication#example-replication-diagram)

For this guide, let's consider the following example:

## [Configuring IT WSUS (RED side)](/docs/netwall/v5.13.2/windows-server-update-service-role-replication-over-netwall-bsg/windows-server-update-service-role-replication#configuring-it-wsus-red-side)

In a normal situation, your IT system administrator controls and configures the IT WSUS (BLUE) server. If you would need additional patches to be downloaded/approved, please notify your IT system administrator and request these to be downloaded for synchronization. Your IT system administrator needs to configure:

- IP address of the WSUS Server
- Port on which WSUS Server listens (default: 8530)
- Whether SSL is enabled/required (default: 8531)

## [Configuring MetaDefender Bilateral Security Gateway RED](/docs/netwall/v5.13.2/windows-server-update-service-role-replication-over-netwall-bsg/windows-server-update-service-role-replication#configuring-metadefender-bilateral-security-gateway-red)

Warning

You need a security dongle plugged in MetaDefender Security Gateway RED to change the configuration.

- Connect to MetaDefender Security Gateway BSG (RED) and login.
- Select Streams -> Action -> Add TCP – depending on whether you want to use SSL or not, select the appropriate port (8530 vs 8531).
- Save the configuration.

## [Configuring MetaDefender Bilateral Security Gateway BLUE](/docs/netwall/v5.13.2/windows-server-update-service-role-replication-over-netwall-bsg/windows-server-update-service-role-replication#configuring-metadefender-bilateral-security-gateway-blue)

Warning

You need a security dongle plugged in MetaDefender Security Gateway RED to change the configuration.

- Connect to MetaDefender Security Gateway (BUE) and login.
- Select Streams -> Action -> Add TCP – depending on whether you want to use SSL or not, select appropriate port (8530 vs 8531). Ensure you use 10 sessions (or more). NOTE: you must match the choice on RED. Example:
- Save the configuration.

## [Configuring WSUS Role on RED side](/docs/netwall/v5.13.2/windows-server-update-service-role-replication-over-netwall-bsg/windows-server-update-service-role-replication#configuring-wsus-role-on-red-side)

This step should be performed by your IT network administrator. If you need specific patches/languages, you will have to ensure these products and classifications are downloaded onto the WSUS on the RED side. You will also need to ensure that your language files are requested. In this example, only small subset of products and classifications is selected on WSUS RED:

The same selection – will be made available on WSUS BLUE – via MetaDefender Security Gateway.

## [Configuring WSUS Role on BLUE](/docs/netwall/v5.13.2/windows-server-update-service-role-replication-over-netwall-bsg/windows-server-update-service-role-replication#configuring-wsus-role-on-blue)

Once the WSUS Role has been installed on BLUE – it must be configured to read from MetaDefender Security Gateway. There are alternatives here. “This server is a replica of the upstream server” checkbox allows you to decide whether this is a “Replica” of the Upstream server or not, as we mentioned in the introduction.

The most straightforward configuration is: No SSL / “Standalone” Server. In that configuration all you need is the MetaDefender Security Gateway BLUE IP Address and port on which you’ve created the bilateral stream. For example:

Click “OK” and Synchronize your server.

Note

The first synchronization will take some time.

Once this is configured and successful synchronization is performed, proceed with using the WSUS BLUE as required.

If you choose to perform SSL synchronization, additional steps are needed in order to establish trust. On the RED Server, open IIS (Internet Information Services) manager and create/bind self-signed certificate.

1. On the BLUE Server, import the certificate that the RED IIS presents to the Local Computer Store, depending on the certificate type you may need to import it to various locations. Check below an example for a self-signed certificate:

2. Use text editor (for example Notepad) to edit hosts file in: C:\Windows\System32\drivers\etc\hosts. Create an entry matching the name of the WSUS RED server, place the IP address of the MetaDefender Security Gateway BLUE and save it. For example:

3. In your WSUS Role on BLUE, Update Source and Proxy Server; select the name of the server (as in step 3) and port and check “Use SSL” box. For example:

4. Perform Synchronization to ensure the operation of the WSUS Role BLUE.

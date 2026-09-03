<!-- source: https://www.opswat.com/docs/filescan/3.1.1/installation/network-setup -->

# Network Setup

### [High-Level Networking Setup](/docs/filescan/3.1.1/installation/network-setup#high-level-networking-setup)

It is strongly recommended to deploy the **MetaDefender Aether** (previously known as MetaDefender Sandbox) server in a **segregated network** (e.g. DMZ, VLAN, VPC).

This segregated network can be connected to a corporate network through a firewall that only allows access to the Sandbox Web interface and REST API over **HTTPS (port 443)**. This "management" connection might use a dedicated network interface.

Optionally, a secondary network interface could be used for "sample analysis" purposes to allow outbound connections to the Internet. An important purpose of the Sandbox system is to download the second stage payloads and analyze them. This secondary network connection can also be used for updating system packages, downloading updated YARA rules and connecting to reputation services in the Cloud.

An Internet connection is needed for a normal online product installation. [Offline Installation](/docs/filescan/3.1.1/installation/offline-installation) is also possible after preparing the necessary installation assets. After a successful installation, the outbound connection might be disabled after considering the following limitations:

- Offline systems cannot receive updated features (like YARA rules) to improve detections for recent threats.
- All third-party integrations (e.g. Reputation API, geolocation/WHOIS lookup) require an Internet connection.
- The "File download" feature is not available in offline environments.
- The "URL rendering and phishing detection" features are not available in offline environments.

Note that the quality of the Sandbox analysis will deteriorate without these important features!

### [Recommended iptables Configuration](/docs/filescan/3.1.1/installation/network-setup#recommended-iptables-configuration)

The following `iptables` rules are recommended for a standard single-server deployment.

This setup will block all incoming connections except for HTTPS (port 443) and SSH (port 22) traffic.

We also need to allow internal communication on the `docker0` interface, otherwise the Sandbox Webservice cannot send requests to Sandbox Broker running on the host system.

Please fine-tune these rules to match your specific requirements:

# Set default policies
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT
# Accept traffic on localhost
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT
# Allow established sessions to receive traffic
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
# Allow outside access to the Sandbox Webservice and REST API
iptables -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT
# Allow Sandbox Webservice to reach Sandbox Broker on docker0 interface
iptables -A INPUT -d 172.17.0.1/16 -j ACCEPT
# (Optional) Allow SSH access
iptables -A INPUT -p tcp -m tcp --dport 22 -j ACCEPT
#### [Additional Hardening](/docs/filescan/3.1.1/installation/network-setup#additional-hardening)

It is also possible to block all outgoing traffic except for a selected list of domains. Please refer to the list of [Domains Contacted During Installation & Operation](/docs/filescan/3.1.1/installation/domains-contacted-during-installation) to identify the most important domains.

Warning

Disclaimer: With maximum hardening the analysis quality will decrease, as the purpose of the sandbox is to allow outbound traffic to download the second stage payloads and analyze them.

Note that `iptables` alone is not suitable for blocking/allowing connections on the domain level (iptables works with IP addresses instead).

### [Internal Communication Ports](/docs/filescan/3.1.1/installation/network-setup#internal-communication-ports)

All internal communication among Sandbox components uses custom REST APIs.

The `broker` HTTP server is listening on port 23001.

The `transform` HTTP server is listening on port 22001.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/getting-started/use-cases -->

# Use Cases and Integrations

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [**MetaDefender ICAP Server Use Cases**](/docs/mdicap/v5.15.0/getting-started/use-cases#metadefender-icap-server-use-cases)

MetaDefender ICAP Server integrates into your existing network devices to provide an additional layer of security for file uploads, file downloads, and file transfers. It is designed to prevent malware outbreaks, data breaches, and compliance violations by scanning files for malware, vulnerabilities, and sensitive data at the network perimeter.

Common use cases where MetaDefender ICAP Server is deployed alongside a network security device to secure the file uploads and transfers moving through the network traffic:

- Productivity documents (PDF, Microsoft Office, etc.)
- Archived files
- Banking, mortgage forms
- Contracts, invoices
- Insurance claims
- Patient portal, records
- Applications, resumes
- Client portals
- Court documents, tax forms
- Unemployment forms
- College assignments
- Collaboration tools (MFT, Dropbox, etc.)

### [Common Integration Points](/docs/mdicap/v5.15.0/getting-started/use-cases#common-integration-points)

#### [**Reverse Proxy and Load Balancer**](/docs/mdicap/v5.15.0/getting-started/use-cases#reverse-proxy-and-load-balancer)

Protect application web servers from malicious file upload. Set up your reverse proxy or load balancer to automatically forward any uploaded files to MetaDefender ICAP Server. This integration ensures that all incoming files undergo thorough scanning and analysis before reaching the intended destination.

Supports:

- F5 BIG-IP Local Traffic Manager (LTM)
- NGINX Plus, NGINX Open Source
- Symantec ProxySG (Blue Coat)
- Squid Web Gateway

#### [**Ingress Controller**](/docs/mdicap/v5.15.0/getting-started/use-cases#ingress-controller)

Enhance efficient application delivery in the cloud, security posture and compliance adherence by integrating MetaDefender ICAP Server with an ingress controller. By inspecting all incoming files for malicious content, organizations can mitigate the risk of data breaches and ensure the integrity of their web servers, applications, and customer portals.

Supports:

- NGINX Plus, NGINX Open Source

#### [**Web Application Firewall (WAF)**](/docs/mdicap/v5.15.0/getting-started/use-cases#web-application-firewall-waf)

Strengthen defense mechanisms against cyber threats by combining the threat prevention capabilities of both MetaDefender ICAP Server with a WAF. Leverage this multi-layered security approach to effectively mitigate risks associated with file-based attacks and web-based attacks.

Supports:

- F5 BIG-IP Advanced Firewall Manager (AFM)
- F5 BIG-IP Application Security Manager (ASM)
- NGINX App Protect
- Fortinet Fortigate Next Generation Firewall (NGFW)
- VMware Avi Vantage

#### [**Application Delivery Controller (ADC)**](/docs/mdicap/v5.15.0/getting-started/use-cases#application-delivery-controller-adc)

Safeguard the integrity of web-based systems. Ensure web applications are optimized to run smoothly while all files uploaded through the application are secured. MetaDefender ICAP Server helps mitigate the risk of data breaches and defends against attacks leveraging file-borne malware or zero-day exploits.

Supports:

- F5 BIG-IP Local Traffic Manager (LTM)
- NetScaler ADC (formerly Citrix ADC)

#### [**Secure Sockets Layer (SSL) Inspector**](/docs/mdicap/v5.15.0/getting-started/use-cases#secure-sockets-layer-ssl-inspector)

Integrate MetaDefender ICAP Server at the point of decryption to ensure protection against sophisticated cyber attacks and regulatory compliance. By intercepting and inspecting SSL/TLS traffic, organizations can gain network traffic visibility and eliminate the blind spots hidden within uploaded files and encrypted communications.

Supports:

- F5 BIG-IP SSL Orchestrator
- A10 Networks Thunder SSLi

#### [**Managed File Transfer (MFT)**](/docs/mdicap/v5.15.0/getting-started/use-cases#managed-file-transfer-mft)

This integration enables proactive inspection of file content. Scan all file traffic as it moves through your data repositories to enhance data security during file transfer. Files remain safe to be transferred. Sensitive information remains protected throughout the transfer process, ensuring compliance and confidentiality.

Supports:

- GoAnywhere MFT
- Progress MOVEit
- Axway B2Bi
- GlobalScape EFT
- FileCloud Server

#### [**Storage Solutions**](/docs/mdicap/v5.15.0/getting-started/use-cases#storage-solutions)

Ensure the integrity and security of file sharing in data storage. Consistently scan files in repositories on read, write, or at rest. By integrating MetaDefender ICAP Server with storage solutions, organizations can proactively identify and remove malicious content, minimizing the risk of data corruption and unauthorized access.

Supports:

- Dell EMC Isilon OneFS
- Nutanix Files
- Huawei Oceanstor

#### [**Web Gateways**](/docs/mdicap/v5.15.0/getting-started/use-cases#web-gateways)

Screen file content in web traffic before it reaches secured networks. By integrating MetaDefender ICAP Server with web gateways, organizations can enforce security policies and prevent the infiltration of malware, phishing attempts, and other malicious activities.

Supports:

- ARA Networks JAGUAR5000
- McAfee Web Gateway
- Symantec ProxySG (Blue Coat)
- Squid Web Gateway
- Forcepoint Secure Web Gateway
- Airlock Secure Access Hub Gateway
- Cyolo Secure Remote Access (SRA)

#### [**Forward Proxy**](/docs/mdicap/v5.15.0/getting-started/use-cases#forward-proxy)

Set up any forward proxy that implements ICAP to automatically send HTTP requests to MetaDefender ICAP Server. Allows the firewall to offload work to a separate server specifically set up for the specialized processing of the incoming traffic.

Supports:

- Squid Open Proxy
- Symantec ProxySG (Blue Coat)
- Forcepoint

#### [**Intrusion Prevention Systems (IPS)**](/docs/mdicap/v5.15.0/getting-started/use-cases#intrusion-prevention-systems-ips)

Augment the effectiveness of IPS/IDS solutions with MetaDefender ICAP Server's advanced threat detection and prevention capabilities. By analyzing incoming files for known vulnerabilities, zero-day exploits, and suspicious behavior, organizations can proactively identify and mitigate potential security threats, reducing the risk of data breaches and system compromise.

Supports:

- Any IPS/IDS with ICAP client functionality

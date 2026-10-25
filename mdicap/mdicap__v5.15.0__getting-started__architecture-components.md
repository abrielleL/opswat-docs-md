<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/getting-started/architecture-components -->

# Architecture & Components

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender ICAP Server is built upon the Internet Content Adaptation Protocol (ICAP) defined in [RFC 3507](https://datatracker.ietf.org/doc/html/rfc3507). ICAP Server functions as a simplified, plug and play connector between a network security device with an ICAP client, e.g. a load balancer, WAF, MFT, SRA or ingress controller, and MetaDefender Core which performs the file analysis. Integrating via ICAP offers the ability to easily incorporate advanced file security without requiring any network architecture changes or API scripting.

## [High-Level Integration Diagram](/docs/mdicap/v5.15.0/getting-started/architecture-components#high-level-integration-diagram)

## [Components](/docs/mdicap/v5.15.0/getting-started/architecture-components#components)

- **3rd-party network security device** with an ICAP client. Multiple ICAP clients can be connected to the same ICAP Server to support multiple file workflows in transit or at rest.

  - When files are upload to a protected web application, or accessed within a protected MFT or storage device, the ICAP client will identify files which need to be scanned and then will forward those files to the ICAP server for processing by the backend MetaDefender Core server.
  - Once a result is received from the ICAP server, the network device will allow the file, drop the file, or take other actions configured within the network device.
- **MetaDefender ICAP Server** functions as the lightweight interface between the network device and the scanning backend. A single MetaDefender ICAP Server can connect to multiple MetaDefender Core servers for scalability and resiliency.

  - When files are sent by the ICAP client, the ICAP Server will receive the files and then pass to MetaDefender Core for analysis.
  - Once MetaDefender Core completes the analysis and provides a result, the result will be passed to the ICAP client for further processing by the network device.
- **MetaDefender Core** is the file analysis backend which performs multiscanning, content disarm and reconstruction (CDR), DLP and other advanced file security functions. In addition to ICAP Server integration, MetaDefender Core offers a full REST API to integrate directly with custom applications.

  - When files are received from MetaDefender ICAP Server, MetaDefender Core will process the files according to the configured workflow and provide a result.
  - Once the scan tasks are completed, the file analysis result is delivered to ICAP Server.

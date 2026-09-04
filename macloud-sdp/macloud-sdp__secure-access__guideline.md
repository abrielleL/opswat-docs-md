<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/guideline -->

# Guideline

In addition to other approaches to securing applications, MetaDefender IT-OT Access now also offers SDP approach for Secure IT Access.

The SDP approach to zero trust networking flips the traditional approach of securing access to network resources on its head. Instead of connecting then authorizing, the client is required to first authenticate, authorize, be checked for compliance, and only then is it allowed access.

Info

The SDP approach to controlling access is part of the Secure IT Access module offered as an additional purchase on top of the base MetaDefender IT-OT Access offering. You can learn more [here](https://www.opswat.com/uploads/assets/files/Product-Guide_compressed-1.pdf).

For those not familiar with SDPs, the main take away is they are better than a traditional VPN in that they are better in the following ways:

Secure Apps for remote or on-premise access:

- Applications invisible — No access until authorized
- Prevents the most common attacks like DDoS
- Perimeter of one leveraging PKI, mTLS tunnels

SDP is a better VPN Alternative in that SDP is:

- Easier to deploy, scale – choose between a OPSWAT Hosted Secure IT Access Gateway (additional charge) or an included Private Secure IT Access Gateway that can be easily deployed as a virtual appliance, and scaled out through use of multiple instance to handle additional load.

- Easer, modern management – leverages tight integration with your existing Identity Access Mechanism (IAM).
- More secure by leveraging a number of advance techniques, such as Single Packet Authentication to permit the access gateway to be completely dark to potential attackers (effectively a “Deny All” firewall).

The diagram below explains how SDP works at a high-level:

1. Traditionally, hackers had a wide attack surface through a firewall VPN or LAN connection
2. Zero trust is layered on through a DENY ALL, **Access Gateway** in front of applications
3. A **Trust Broker** (controller) acts as an intermediary
4. Before **Clients** connect to applications, trust policies are checked. With SDP, only then can the **Clients** connect.

Info

For more detail, including an option to download a whitepaper, visit the [Secure](https://www.opswat.com/products/metaaccess/metaaccess-sdp) [Access](https://www.opswat.com/products/metadefender/it-ot-access/secure-access-it) [for IT page](https://www.opswat.com/products/metaaccess/metaaccess-sdp) on [opspwat.com](http://opspwat.com).

<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/introduction -->

# Introduction

In addition to other approaches to securing applications, My OPSWAT Central Management now also offers SDP approach for Secure IT Access.

The SDP approach to zero trust networking flips the traditional approach of securing access to network resources on its head. Instead of connecting then authorizing, the client is required to first authenticate, authorize, be checked for compliance, and only then is it allowed access.

> **Info**
>
> The SDP approach to controlling access is part of the My OPSWAT Central Management module offered as an additional purchase on top of the base My OPSWAT Central Management offering. You can learn more [here](https://www.opswat.com/uploads/assets/files/Product-Guide_compressed-1.pdf).

For those not familiar with SDPs, the main take away is they are better than a traditional VPN in the following ways:

Secure Apps for remote or on-premise access:

- Applications invisible — No access until authorized
- Prevents the most common attacks like DDoS
- Perimeter of one leveraging PKI, mTLS tunnels `(TLS-DHE-RSA-WITH-AES-256-CBC-SHA256)`

SDP is a better VPN Alternative in that SDP is:

- Easier to deploy, scale – choose between a OPSWAT Hosted Secure IT Access Gateway (additional charge) or an included Private Secure IT Access Gateway that can be easily deployed as a virtual appliance, and scaled out through use of multiple instance to handle additional load.

![](https://uploads.developerhub.io/prod/97qW/cnkpvu76dmv6q2s3xsz1wst1brwnkv3575y56d4z9zv447idwjafvro4fll9p0c6.png)

- Easer, modern management – leverages tight integration with your existing Identity Access Mechanism (IAM).
- More secure by leveraging a number of advance techniques, such as Single Packet Authentication to permit the access gateway to be completely dark to potential attackers (effectively a “Deny All” firewall).

The diagram below explains how SDP works at a high-level:

1. Traditionally, hackers had a wide attack surface through a firewall VPN or LAN connection
2. Zero trust is layered on through a DENY ALL, **Access Gateway** in front of applications
3. A **Trust Broker** (controller) acts as an intermediary
4. Before **Clients** connect to applications, trust policies are checked. With SDP, only then can the **Clients** connect.

![](https://uploads.developerhub.io/prod/97qW/5zhalvi4syusrybso9yvuncfb8bmkwb0xnnkcibj3szreue3vzqmalrvzpa0wghd.png)

> **Info**
>
> For more detail, including an option to download a whitepaper, visit the [Secure ](https://www.opswat.com/products/metaaccess/metaaccess-sdp)[Access ](https://www.opswat.com/products/metadefender/it-ot-access/secure-access-it)[for IT](https://www.opswat.com/products/metaaccess/metaaccess-sdp) on [opswat.com](http://opspwat.com).

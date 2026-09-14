<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/what-links--target-services-or-target-host-ip-s-need-to-be-allow -->

# What links, target-services or target host-IPs need to be allowed for Metadefender Core to function accurately?

This article applies to all MetaDefender Core V5 releases deployed on Windows or Linux systems.

If you have installed, or if you wish to install or use, the MetaDefender Core system in a restricted environment, you will have to allow access to the following hosts' to ensure MetaDefender Core’s accurate functioning:

- [https://activation.dl.opswat.com](https://activation.dl.opswat.com/) - this is for product activation/licensing.
- [https://update.dl.opswat.com](https://update.dl.opswat.com/) - this is for fetching engine/database updates.

Attention:

Since August 2023, we've migrated to AWS Cloudfront as our CDN for Update Servers. Depending on your location, you'll be directed to specific Edge Locations, each with its own unique IP ranges. Ensure you've allowed the correct Cloudfront IP ranges by referring to: <https://ip-ranges.amazonaws.com/ip-ranges.json>

Pro Tip:

Even though the OPSWAT update servers host updates for all of the available engines we support, the custom engines might occasionally try to connect to their own cloud for updates.

This can be disabled under **Firewall**, after which the engines will only be updated via OPSWAT.

Configure MetaDefender Core’s proxy configuration settings if applicable for update server and activation server URLs.

Please Note:

IP address based allowlisting might fail after some time, since OPSWAT employs a **CDN (Content Delivery Network)** to achieve faster updates globally, and the IP addresses of edge servers might change over time.

Info:

If the internal policy requires certificate validation, the firewall must allow access to the CRL and OCSP URLs of the OPSWAT Activation and Engine Update servers' certificates, as well as their Intermediate CA (ICA) certificate. To extract the URLs that need whitelisting, please follow [How to retrieve the CRL and OCSP URLs for the Server and ICA Certificates?](/docs/mdcore/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer)

Support:

If you have any difficulty **Installing** and **Setting Up** MetaDefender Core in a restricted environment, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).

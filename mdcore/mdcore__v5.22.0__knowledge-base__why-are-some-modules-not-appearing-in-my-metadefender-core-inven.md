<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-are-some-modules-not-appearing-in-my-metadefender-core-inven -->

# Why are some modules not appearing in my MetaDefender Core inventory?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

If your inventory does not include all of the modules that are listed as part of your MetaDefender Core package license, this is likely indicative that the system is deployed offline (in a restricted environment) and is unable to connect to the necessary OPSWAT hosts for initial module activation and regular updates.

For offline environments, the Core deployment requires an import YAML license into the activation tab for the engines as well as engines download using [MetaDefender Update Downloader](https://www.opswat.com/docs/mddownloader) to be successfully deployed.

Pro Tip:

If you have installed or if you wish to use the MetaDefender Core in an online environment, you will have to allow access to the following hosts' for accurate functioning of all included modules:

- [https://activation.dl.opswat.com](https://activation.dl.opswat.com/) - this is for product activation/licensing
- [https://update.dl.opswat.com](https://update.dl.opswat.com/) - this is for fetching engine/database updates
Please Note:

IP address-based whitelisting on your firewall might fail after some time, since OPSWAT uses CDN (Content Delivery Network) to faster deliver updates around the globe, and IP addresses of edge servers might change over time.

Info:

If the internal policy requires certificate validation, the firewall must allow access to the CRL and OCSP URLs of the OPSWAT Activation and Engine Update servers' certificates, as well as their Intermediate CA (ICA) certificate. To extract the URLs that need whitelisting, please follow [How to retrieve the CRL and OCSP URLs for the Server and ICA Certificates?](/docs/mdcore/v5.22.0/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer)

If the issue is network related, please keep in mind that, in an online environment where MetaDefender Core is configured to download module and scan engine update packages directly from an OPSWAT update server source, using a gigabit network speed (125MB/sec) is highly recommended to avoid potential network related issues during file downloads. The same is true for initial activation downloads.

At the very least, the requirement is a network speed of 100Mbps (12.5MB/sec).

Support:

If you have followed the instructions above but **Some Modules Are Still Not Appearing In Your MetaDefender Core Inventory**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).

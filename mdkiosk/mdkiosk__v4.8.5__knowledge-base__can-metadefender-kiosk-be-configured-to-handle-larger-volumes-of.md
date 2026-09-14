<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/can-metadefender-kiosk-be-configured-to-handle-larger-volumes-of -->

# Can MetaDefender Kiosk be configured to handle large volumes of scans more quickly?

This article applies to all MetaDefender Kiosk V4 releases deployed on Windows or Linux systems.

Yes, it can.

The performance and configuration of the associated MetaDefender Core instance can drastically limit the performance of your MetaDefender Kiosk solution.

Please Note:

MetaDefender Core is greatly affected by its host hardware’s specifications.

Standard Kiosk units are intended to be portable, convenient and easy to set up; as a result, these units are limited in size and airflow, making them more suitable for standard usage with medium traffic.

Customers requiring high volume scans and faster performance should consider a distributed configuration where the MetaDefender Kiosk module is maintained on the Kiosk and the MetaDefender Core module is maintained on a powerful remote server.

The diagram below illustrates the distributed configuration:

Support:

If you are having difficulty **Setting Up a Distributed Configuration for MetaDefender Kiosk**, please follow these instructions on [How To Create a Support Package](https://docs.opswat.com/mdkiosk/troubleshooting#creating-the-package), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).

<!-- source: https://www.opswat.com/docs/mddownloader/installation/system-requirements -->

# System Requirements

OPSWAT will discontinue support for the following OS in MetaDefender Update Downloader:

- Windows 10 after **October 2025**.
- Windows Server 2016 after **October 2025**.

You can stay with these OS and would not see negative impacts during your operation and usage. However, we suggest you move on to newer OS for good measure.

**Only 64-bit platforms are supported.**

- Operating System:

  - Rocky Linux 9.4
  - Debian 12
  - Ubuntu 22.04
  - Windows 11
  - Windows Server 2019, 2022
- Hardware requirements

  - RAM: min. 2 GB
  - HDD: 2 GB + ~500MB * [number of managed scan engines]

    - Note: some engines might have a bigger file size than others, for example: SBOM, Adaptive Sandbox engine will take more than 1GB.
- Third party dependency:

  - Microsoft Visual C++ Redistributable for Visual Studio 2015-2022; x64 version.
- Internet connection required to be able to connect to OPSWAT update servers.

Allowlisting URLs

If you have installed or plan to use the MetaDefender Update Downloader in a restricted environment, you must allow access to the following hosts for engine and database downloads:

- [https://update.dl.opswat.com](https://update.dl.opswat.com/)

**Note:** *IP address-based allowlisting on your firewall may fail over time because OPSWAT uses CDN (AWS Cloudfront) to accelerate global update delivery, and the IP address of edge servers may change periodically.*

*Depending on your location, connections to OPSWAT's cloud-based servers may be forwarded to specific AWS Cloudfront edge locations, each assigned its own unique IP address ranges. You may also need to allow the corresponding* *AWS Cloudfront* *IP address ranges by referring to* [*https://ip-ranges.amazonaws.com/ip-ranges.json*](https://ip-ranges.amazonaws.com/ip-ranges.json)

Warning

Although OPSWAT update servers host updates for all supported engines, some custom engines may attempt to connect to their own cloud for updates. However, this can be blocked at the firewall, ensuring that updates are retrieved exclusively from OPSWAT.

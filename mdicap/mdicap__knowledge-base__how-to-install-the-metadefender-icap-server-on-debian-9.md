<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/how-to-install-the-metadefender-icap-server-on-debian-9 -->

# How to Install the MetaDefender ICAP Server on Debian 9?

## [Symptom of install failure](/docs/mdicap/knowledge-base/how-to-install-the-metadefender-icap-server-on-debian-9#symptom-of-install-failure)

When you install ICAP Server on Debian 9 you may get the following error message:

dpkg: dependency problems prevent configuration of mdicapsrv:
mdicapsrv depends on libssll.O.O (>= 1.0.0); however:
Package libssll.0.0 is not installed.
## [Reason](/docs/mdicap/knowledge-base/how-to-install-the-metadefender-icap-server-on-debian-9#reason)

By default, Debian 9 is installed with libssl1.0.2. For compatibility reasons OPSWAT products require libssl1.0.0. libssl1.0.0 is, however, only available in Debian 8 repositories, and is not available for Debian 9.

## [Resolution](/docs/mdicap/knowledge-base/how-to-install-the-metadefender-icap-server-on-debian-9#resolution)

To install libssl1.0.0 on Debian 9 from a Debian 8 repository perform the following steps:

1. Open <https://packages.debian.org/jessie/libssl1.0.0> in your browser

2. In the "*Downloads"* section, at the bottom of the page, select your server's architecture
3. Select a mirror (<http://security.debian.org/debian-security> in the example) and download the package

# wget http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u12_amd64.deb

4. Install the downloaded package

# dpkg —i libssl1.0.0_1.0.1t-1+deb8u12_amd64.deb

5. Clean-up the previous broken ICAP Server installation (optional)

# apt --fix-broken install

6. Re-install ICAP Server

# dpkg -i mdicapsrv_4.7.0-1_amd64.deb

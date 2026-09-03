<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/how-to-self-compile-squid-v7-to-work-with-icap-on-ubuntu-linux-2 -->

# How to self compile Squid v7 to work with ICAP on Ubuntu Linux 22.04?

This article applies to all MetaDefender ICAP Server releases deployed on Windows and Linux systems.

According to the [MetaDefender ICAP Server documentation](https://www.opswat.com/docs/mdicap/integrations/squid), integrating Squid with ICAP using versions 5.5 through 6.11 may result in a known bug that affects the user experience during file downloads via the RESPMOD request. This issue has been resolved in Squid version 7 and later, and currently Squid doesn’t have a pre-compiled installation package for this version.

Info:

You can also use Squid **4.13** or **6.13** to avoid having this bug.

## [1. Installing prerequisite packages to compile](/docs/mdicap/knowledge-base/how-to-self-compile-squid-v7-to-work-with-icap-on-ubuntu-linux-2#1-installing-prerequisite-packages-to-compile)

HtmlCopysudo apt install build-essential autoconf automake make libtool pkg-config libssl-dev libcppunit-dev libkrb5-dev libsasl2-dev libxml2-dev libcap-dev g++ perl

From Squid 6, you will need any compiler that is C++17-compiliant. These should be available on latest unix and linux distributions. (Read more at [Squid Official Guide](https://wiki.squid-cache.org/SquidFaq/CompilingSquid)).

## [2. Download latest Squid v7 release](/docs/mdicap/knowledge-base/how-to-self-compile-squid-v7-to-work-with-icap-on-ubuntu-linux-2#2-download-latest-squid-v7-release)

[squid : Optimising Web Delivery](https://www.squid-cache.org/Versions/v7/)

After downloading the archive, extract the contents of the tar file and navigate into the extracted directory.

HtmlCopytar xvf squid-7.0.0-2024xxxx-xxxx.tar
cd squid-7.0.0-VCS/
### [Configure Squid options](/docs/mdicap/knowledge-base/how-to-self-compile-squid-v7-to-work-with-icap-on-ubuntu-linux-2#configure-squid-options)

HtmlCopy./configure \
--prefix=/usr \
--localstatedir=/var \
--libexecdir=/usr/lib/squid \
--datadir=/usr/share/squid \
--sysconfdir=/etc/squid \
--with-default-user=proxy \
--with-logdir=/var/log/squid \
--with-pidfile=/var/run/squid.pid \
--enable-ssl \
--enable-security-file-certgen \
--enable-icap-client \
--enable-http-violations \
--with-openssl \
--enable-linux-netfilterInfo:

**You must have “**`--enable-ssl --enable-security-file-certgen --with-openssl`**" options if you wish to use ICAPS (ICAP Secured with TLS).**

### [Explanation of Key Options](/docs/mdicap/knowledge-base/how-to-self-compile-squid-v7-to-work-with-icap-on-ubuntu-linux-2#explanation-of-key-options)

- `--prefix`, `--localstatedir`, `--sysconfdir`: Define installation paths for Squid binaries, configuration files, logs, and runtime data.
- `--with-default-user=proxy`: Runs Squid under the `proxy` user for better security isolation.
- `--enable-icap-client`: Enables ICAP protocol support for content adaptation.
- `--enable-ssl`, `--with-openssl`: Adds SSL/TLS support, required for HTTPS and ICAPS.
- `--enable-security-file-certgen`: Enables on-the-fly certificate generation for SSL bumping.
- `--enable-http-violations`: Allows flexibility in HTTP protocol behavior, useful for advanced proxy configurations.
- `--enable-linux-netfilter`: Enables Netfilter (iptables) integration for transparent proxying.

### [Output Paths](/docs/mdicap/knowledge-base/how-to-self-compile-squid-v7-to-work-with-icap-on-ubuntu-linux-2#output-paths)

Once configured and built with the options above:

- Configuration files will be located at: `/etc/squid/squid.conf`
- Log files will be available at: `/var/log/squid`

## [3. Compile & Install Squid](/docs/mdicap/knowledge-base/how-to-self-compile-squid-v7-to-work-with-icap-on-ubuntu-linux-2#3-compile--install-squid)

To compile Squid, run the below command:

HtmlCopymake

After the compilation has finished, run the below command to install Squid into your system:

HtmlCopysudo make install
## [4. Verify Squid installation](/docs/mdicap/knowledge-base/how-to-self-compile-squid-v7-to-work-with-icap-on-ubuntu-linux-2#4-verify-squid-installation)

You can verify Squid has been installed successfully by using `squid -v` command

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

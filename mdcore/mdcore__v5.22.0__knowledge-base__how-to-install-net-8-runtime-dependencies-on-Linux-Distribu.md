<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-install-net-8-runtime-dependencies-on-Linux-Distribu -->

# How to install .NET 8 Runtime dependencies on Linux Distributions?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Linux systems.

Pro Tip:

Linux Distributions usually have .NET dependencies installed in their system, if the engines failed to load, please follow the steps below to install

## [Red Hat Enterprise Linux 8.x](/docs/mdcore/v5.22.0/knowledge-base/how-to-install-net-8-runtime-dependencies-on-Linux-Distribu#red-hat-enterprise-linux-8x)

BashCopysudo yum install libnsl
sudo dnf install krb5-libs libicu openssl-libs zlib
## [Red Hat Enterprise Linux 9.x / Rocky Linux 9](/docs/mdcore/v5.22.0/knowledge-base/how-to-install-net-8-runtime-dependencies-on-Linux-Distribu#red-hat-enterprise-linux-9x--rocky-linux-9)

BashCopysudo yum install libnsl
sudo dnf install krb5-libs libicu openssl-libs zlib
sudo dnf install compat-openssl11
## [Debian 11.x](/docs/mdcore/v5.22.0/knowledge-base/how-to-install-net-8-runtime-dependencies-on-Linux-Distribu#debian-11x)

BashCopywget https://packages.microsoft.com/config/debian/11/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
sudo apt update
sudo apt install dotnet-runtime-deps-8.0
## [Debian 12.x](/docs/mdcore/v5.22.0/knowledge-base/how-to-install-net-8-runtime-dependencies-on-Linux-Distribu#debian-12x)

BashCopywget https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
sudo apt update
sudo apt install dotnet-runtime-deps-8.0
## [Ubuntu 22.04](/docs/mdcore/v5.22.0/knowledge-base/how-to-install-net-8-runtime-dependencies-on-Linux-Distribu#ubuntu-2204)

BashCopywget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
sudo apt update
sudo apt install dotnet-runtime-deps-8.0
## [Amazon Linux 2003](/docs/mdcore/v5.22.0/knowledge-base/how-to-install-net-8-runtime-dependencies-on-Linux-Distribu#amazon-linux-2003)

BashCopysudo dnf install krb5-libs libicu openssl-libs zlibSupport:

If you have followed the instructions above and were unable to install .**NET Runtime dependencies on Linux Distributions**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form.

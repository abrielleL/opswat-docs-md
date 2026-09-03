<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/how-to-install-opswat-central-management-on-ubuntu-20-04-and-22- -->

# How to Install OPSWAT Central Management on Ubuntu 20.04/22.04 and Debian 11/12?

As noted in [Software Requirement](/docs/ocm/installation/recommended-system-requirements#software-requirement), OPSWAT Central Management does not officially support Ubuntu 20.04/22.04 and Debian 11/12. However, installation workarounds are available and described below.

### [Ubuntu 20.04](/docs/ocm/knowledgebase/how-to-install-opswat-central-management-on-ubuntu-20-04-and-22-#ubuntu-2004)

To install OPSWAT Central Management on Ubuntu 20.04, the system must have the package libssl1.0.0 installed, which was removed from official support for Ubuntu 20.04.

libssl1.0.0 is locatedin [the Ubuntu repository](http://security.ubuntu.com/ubuntu/pool/main/o/openssl1.0/). Please install the latest amd64 version of the package. As of March 2024, this is [the most current version](http://security.ubuntu.com/ubuntu/pool/main/o/openssl1.0/libssl1.0.0_1.0.2n-1ubuntu5.13_amd64.deb).

Please note that the download link above may not work indefinitely as new versions are made available.

After installing the libssl1.0.0 package, please follow the [OPSWAT Central Management on Ubuntu installation guide.](/docs/ocm/installation/on-ubuntu)

### [Ubuntu 22.04](/docs/ocm/knowledgebase/how-to-install-opswat-central-management-on-ubuntu-20-04-and-22-#ubuntu-2204)

To install OPSWAT Central Management on Ubuntu 22.04, in addition to libssl1.0.0, the system must also have the package libssl1.1 installed, which was removed from official support for Ubuntu 22.04.

libssl1.0.0 is locatedin [the Ubuntu repository](http://security.ubuntu.com/ubuntu/pool/main/o/openssl1.0/). Please install the latest amd64 version of the package. As of March 2024, this is [the most current version](http://security.ubuntu.com/ubuntu/pool/main/o/openssl1.0/libssl1.0.0_1.0.2n-1ubuntu5.13_amd64.deb).

libssl1.1 is locatedin [the Ubuntu repository](http://security.ubuntu.com/ubuntu/pool/main/o/openssl/). Please install the latest amd64 version of the package. As of March 2024, this is [the most current version](https://security.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.22_amd64.deb).

Please note that the download link above may not work indefinitely as new versions are made available.

After installing the libssl1.0.0 and libssl1.1 packages, please follow the [OPSWAT Central Management on Ubuntu installation guide.](/docs/ocm/installation/on-ubuntu)

### [Debian 11/12](/docs/ocm/knowledgebase/how-to-install-opswat-central-management-on-ubuntu-20-04-and-22-#debian-1112)

To install OPSWAT Central Management on Debian 11/12, the system must have the package libssl1.0.0 installed, which was removed from official support for Debian 11/12.

libssl1.0.0 is locatedin [the Debian repository](https://archive.debian.org/debian/pool/main/o/openssl). Please install the latest amd64 version of the package. As of July 2024, this is [the most current version](https://archive.debian.org/debian/pool/main/o/openssl/libssl1.0.0_1.0.2l-1~bpo8+1_amd64.deb).

Please note that you may also need to install its dependency [multiarch-support](https://archive.debian.org/debian/pool/main/g/glibc/). As of July 2024, this is [the most current version](https://archive.debian.org/debian/pool/main/g/glibc/multiarch-support_2.28-10+deb10u1_amd64.deb).

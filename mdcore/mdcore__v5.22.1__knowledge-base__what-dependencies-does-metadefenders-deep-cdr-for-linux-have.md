<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/what-dependencies-does-metadefenders-deep-cdr-for-linux-have -->

# What dependencies does MetaDefender’s Deep CDR for Linux have?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core releases deployed on Linux systems.

From Deep CDR engine version 8.0.2, MetaDefender’s **Deep CDR** for Linux will no longer require libgdiplus to be preinstalled.

Starting with version 6.0 (released in December 2021), MetaDefender’s **Deep CDR** for Linux will require that **libgdiplus** be pre-installed**.**

**Please follow the relevant instructions below to install libgdiplus on your Linux system:**

#### [Rocky Linux 9.x](/docs/mdcore/v5.22.1/knowledge-base/what-dependencies-does-metadefenders-deep-cdr-for-linux-have#rocky-linux-9x)

- Download the prebuilt [libgdiplus6.0.4.tar.gz](https://installer-cdn.opswat.com/Metadefender/engines/cdr/libgdiplus6.0.4.tar.gz) .

  - File size: 1,857,019 bytes
  - MD5: 759a6a3641a1bc83363336f860cd7f25
  - SHA256: 222ec848c62bdc886ebed980f87d4e56ff3341c5e9af1c242a2e9706b674a4b5
- Run these commands to install, be aware of the “Copy and extract libgdiplus6.0.4.tar.gz ...” step.

BashCopy### Install runtime dependency
dnf install -y 'dnf-command(config-manager)'
dnf config-manager --set-enabled crb
dnf makecache
dnf install -y tar giflib-devel libjpeg-devel giflib libjpeg libpng cairo libtiff libexif glib2
### Copy and extract libgdiplus6.0.4.tar.gz file to your installed folder (this folder can be read by metascan) (for example :/var/lib/libgdiplus6)
mkdir /var/lib/libgdiplus6
tar -xvf libgdiplus6.0.4.tar.gz -C /var/lib/libgdiplus6
echo "/var/lib/libgdiplus6/6.0.4/lib" | sudo tee /etc/ld.so.conf.d/libgdiplus.conf
ldconfig
### Double check libgdiplus was installed successfully
ldconfig -p | grep libgdiplus
### Restart Core to make change applied
systemctl stop ometascan
systemctl start ometascan
#### [Rocky Linux 10.x](/docs/mdcore/v5.22.1/knowledge-base/what-dependencies-does-metadefenders-deep-cdr-for-linux-have#rocky-linux-10x)

- Download the prebuilt <libgdiplus6.0.4_rl10.tar.gz>.

  - File size: 2,541,804 bytes
  - MD5: 4228c639a307fbdb8f735b29ada1ba42
  - SHA256: 8c340a8e95daaaa968766768e462f3b5e87a32c700c17a357b6a3fd4dce310b9
- Run these commands to install, be aware of the “Copy and extract libgdiplus6.0.4_rl10.tar.gz ...” step.

TerminalCopy### Copy and extract libgdiplus6.0.4_rl10.tar.gz file to your installed folder (this folder can be read by metascan) (for example :/var/lib/libgdiplus6)
mkdir /var/lib/libgdiplus6
tar -xvf libgdiplus6.0.4_rl10.tar.gz -C /var/lib/libgdiplus6
echo "/var/lib/libgdiplus6/6.0.4/lib" | sudo tee /etc/ld.so.conf.d/libgdiplus.conf
ldconfig
### Double check libgdiplus was installed successfully
ldconfig -p | grep libgdiplus
### Restart Core to make change applied
systemctl stop ometascan
systemctl start ometascan
#### [**Ubuntu 22.04**](/docs/mdcore/v5.22.1/knowledge-base/what-dependencies-does-metadefenders-deep-cdr-for-linux-have#ubuntu-2204)

BashCopysudo apt install gnupg ca-certificates
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
sudo apt update
sudo apt install libgdiplus
#### [**Ubuntu 24.04**](/docs/mdcore/v5.22.1/knowledge-base/what-dependencies-does-metadefenders-deep-cdr-for-linux-have#ubuntu-2404)

BashCopysudo apt install wget
sudo wget http://ftp.de.debian.org/debian/pool/main/libw/libwebp/libwebp6_0.6.1-2.1+deb11u2_amd64.deb
sudo wget http://ftp.de.debian.org/debian/pool/main/libj/libjpeg-turbo/libjpeg62-turbo_2.1.5-4_amd64.deb
sudo wget http://ftp.de.debian.org/debian/pool/main/t/tiff/libtiff5_4.2.0-1+deb11u5_amd64.deb
sudo wget http://ftp.de.debian.org/debian/pool/main/libg/libgdiplus/libgdiplus_6.0.4+dfsg-2_amd64.deb
sudo dpkg -i libwebp6_0.6.1-2.1+deb11u2_amd64.deb || sudo apt-get install -f
sudo dpkg -i libjpeg62-turbo_2.1.5-4_amd64.deb || sudo apt-get install -f
sudo dpkg -i libtiff5_4.2.0-1+deb11u5_amd64.deb || sudo apt-get install -f
sudo dpkg -i libgdiplus_6.0.4+dfsg-2_amd64.deb || sudo apt-get install -f
#### [**Red Hat 8**](/docs/mdcore/v5.22.1/knowledge-base/what-dependencies-does-metadefenders-deep-cdr-for-linux-have#red-hat-8)

BashCopyrpmkeys --import "http://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF"
su -c 'curl https://download.mono-project.com/repo/centos8-stable.repo | tee /etc/yum.repos.d/mono-centos8-stable.repo'
yum install libgdiplus
#### [**Red Hat 9**](/docs/mdcore/v5.22.1/knowledge-base/what-dependencies-does-metadefenders-deep-cdr-for-linux-have#red-hat-9)

BashCopysudo subscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms
sudo dnf -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
sudo dnf -y install libgdiplus
#### [**Debian 12**](/docs/mdcore/v5.22.1/knowledge-base/what-dependencies-does-metadefenders-deep-cdr-for-linux-have#debian-12)

BashCopysudo apt install wget
sudo wget http://ftp.de.debian.org/debian/pool/main/libw/libwebp/libwebp6_0.6.1-2.1+deb11u2_amd64.deb
sudo wget http://ftp.de.debian.org/debian/pool/main/t/tiff/libtiff5_4.2.0-1+deb11u5_amd64.deb
sudo wget http://ftp.de.debian.org/debian/pool/main/libg/libgdiplus/libgdiplus_6.0.4+dfsg-2_amd64.deb
sudo dpkg -i libwebp6_0.6.1-2.1+deb11u2_amd64.deb || sudo apt-get install -f
sudo dpkg -i libtiff5_4.2.0-1+deb11u5_amd64.deb || sudo apt-get install -f
sudo dpkg -i libgdiplus_6.0.4+dfsg-2_amd64.deb || sudo apt-get install -f
#### [**Amazon Linux 2023**](/docs/mdcore/v5.22.1/knowledge-base/what-dependencies-does-metadefenders-deep-cdr-for-linux-have#amazon-linux-2023)

BashCopysudo curl https://download.mono-project.com/repo/centos8-stable.repo | sudo tee /etc/yum.repos.d/mono-centos8-stable.repo
sudo dnf install libgdiplusSupport:

If you have followed the steps above but are still having trouble installing **Libgdiplus** or running MetaDefender Core’s **Deep CDR** on a Linux system, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.1/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).

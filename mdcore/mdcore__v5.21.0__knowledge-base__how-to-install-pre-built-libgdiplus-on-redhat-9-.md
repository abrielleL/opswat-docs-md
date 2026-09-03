<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-install-pre-built-libgdiplus-on-redhat-9- -->

# How to install pre-built libgdiplus on RedHat 9?

This article applies to all MetaDefender Core releases deployed on Linux systems.

Installing the pre-built **libgdiplus** package on **Red Hat Enterprise Linux (RHEL) 9** is necessary for running **Deep CDR**. Since **libgdiplus** is not available in the default RHEL repositories and some users may not be able to install it from **EPEL** or **Mono**, using a pre-built version is the best alternative. This guide provides step-by-step instructions for downloading, extracting, and configuring the pre-built **libgdiplus** package to ensure smooth operation of **Deep CDR** on your system.

- Download the prebuilt [libgdiplus6.0.4.tar.gz](https://installer-cdn.opswat.com/Metadefender/engines/cdr/libgdiplus6.0.4.tar.gz) .

  - File size: 1,857,019 bytes
  - MD5: 759a6a3641a1bc83363336f860cd7f25
  - SHA256: 222ec848c62bdc886ebed980f87d4e56ff3341c5e9af1c242a2e9706b674a4b5
- Run these commands to install, be aware of the “Copy and extract libgdiplus6.0.4.tar.gz ...” step.

TerminalCopy### Install runtime dependency
dnf install -y libjpeg-devel giflib libjpeg libpng cairo libtiff libexif glib2
### Copy and extract libgdiplus6.0.4.tar.gz file to your installed folder (this folder can be read by metascan) (for example :/var/lib/libgdiplus6)
mkdir /var/lib/libgdiplus6
tar -xvf libgdiplus6.0.4.tar.gz -C /var/lib/libgdiplus6
echo "/var/lib/libgdiplus6/6.0.4/lib" | sudo tee /etc/ld.so.conf.d/libgdiplus.conf
ldconfig
### Double check libgdiplus was installed successfully
ldconfig -p | grep libgdiplus
### Restart Core to make change applied
systemctl stop ometascan
systemctl start ometascanSupport:

If you have followed the steps above but are still having trouble installing pre-built **libgdiplus**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).

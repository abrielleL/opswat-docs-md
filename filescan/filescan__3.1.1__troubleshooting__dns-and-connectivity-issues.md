<!-- source: https://www.opswat.com/docs/filescan/3.1.1/troubleshooting/dns-and-connectivity-issues -->

# DNS and connectivity issues

If you encounter DNS or Internet connectivity issues during the Sandbox installation process, it is recommended to configure public DNS nameservers (e.g.: `8.8.8.8` or `1.1.1.1`).

If you have a desktop installation, you may configure the DNS settings using the NetworkManager GUI.

If you have a server installation without a desktop environment, you can run the following commands:

BashCopy# Check your current DNS settings in /etc/resolv.conf
cat /etc/resolv.conf
# Install resolveconf and set 8.8.8.8 as primary DNS server
sudo apt update
sudo apt install resolvconf
echo 'nameserver 8.8.8.8' | sudo tee /etc/resolvconf/resolv.conf.d/head
# Update /etc/resolv.conf using resolveconf
sudo resolvconf -u
# Check the updated DNS settings
cat /etc/resolv.conf

If everything went well, you should see something like this (`8.8.8.8` should be the first nameserver in the list):

BashCopynameserver 8.8.8.8
nameserver 127.0.0.53
options edns0 trust-ad

Please also check your DNS settings in a Docker container (`8.8.8.8` should be the first nameserver):

BashCopysudo docker container run --rm busybox cat /etc/resolv.conf

See this guide for more information: [How To Set Permanent DNS Nameservers in Ubuntu and Debian](https://www.tecmint.com/set-permanent-dns-nameservers-in-ubuntu-debian/)

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

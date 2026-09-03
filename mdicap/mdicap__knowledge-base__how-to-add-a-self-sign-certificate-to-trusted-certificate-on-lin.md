<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/how-to-add-a-self-sign-certificate-to-trusted-certificate-on-lin -->

# How to Add a Self-Sign Certificate to Trusted Certificate on Linux?

This is the guideline to adding a self-sign certificate to trusted certificate on Linux

For example We have a self-sign certificate name: **self-sign.crt**

### [**Ubuntu/Debian**](/docs/mdicap/knowledge-base/how-to-add-a-self-sign-certificate-to-trusted-certificate-on-lin#ubuntudebian)

BashCopysudo cp -f self-sign.crt /usr/local/share/ca-certificates
sudo update-ca-certificates
### [**CentOS/RHEL**](/docs/mdicap/knowledge-base/how-to-add-a-self-sign-certificate-to-trusted-certificate-on-lin#centosrhel)

BashCopy#install ca-certificates
sudo yum install -y ca-certificates
#install certificate
cp -f self-sign.crt /etc/pki/ca-trust/source/anchors/
sudo update-ca-trust enable
sudo update-ca-trust extract

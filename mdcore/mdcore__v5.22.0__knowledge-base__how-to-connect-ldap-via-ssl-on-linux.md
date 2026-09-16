<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-connect-ldap-via-ssl-on-linux -->

# How to connect LDAP via SSL on Linux

This article applies to all MetaDefender V5 releases deployed on Linux systems.

There are 2 ways we can config to make MetaDefender Core read the cert using LDAP via SSL connection

Note:

Please use only one method. If you check with local trusted store, please don't use */etc/openldap/ldap.conf*. If you use */etc/openldap/ldap.conf* please check that there is no file *ldap.crt* file in local trusted store also, there is no content of *ldap.crt* file in *ca-bundle.crt*. Please use only one method.

1. We can use a local trusted store, here is how we add crt file to the local trusted store

   1. Deb/Ubuntu:

BashCopycp -f ldap.crt /usr/local/share/ca-certificates
update-ca-certificates

b. Centos/RHEL:

BashCopycp -f ldap.crt /etc/pki/ca-trust/source/anchors/
update-ca-trust enable
update-ca-trust extract

2. If we do not want to use a local trusted store, we also can create a specific configuration file to tell MetaDefender Core where to look for cert

BashCopy#Create file ldap.conf in /etc/openldap/ldap.conf
##Centos/RHEL
echo "TLS_CACERT /path/to/ldap.crt" >> /etc/openldap/ldap.conf
##Debian/Ubuntu
echo "TLS_CACERT /path/to/ldap.crt" >> /etc/ldap/ldap.confSupport:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).

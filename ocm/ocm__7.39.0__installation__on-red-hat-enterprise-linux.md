<!-- source: https://www.opswat.com/docs/ocm/7.39.0/installation/on-red-hat-enterprise-linux -->

# On Red Hat Enterprise Linux

On Red Hat Enterprise Linux system, please follow the below steps to install the OPSWAT Central Management package.

1/ Open the terminal.

2/ Install the rpm package:

sudo yum install <path to .rpm file>Info

For systems which enabled GPD check flag, use the install command below instead:

**sudo yum install --nogpdcheck <path to .rpm file>**

3/ In order for the OPSWAT Central Management systemd service to locate environment variables such as

**http_proxy**, the **EnvironmentFile** setting must be specified in the service file located at /usr/lib/ocm/ocm.service.

a/ Locate the commented out **EnvironmentFile** settings in **/usr/lib/ocm/ocm.service**

#EnvironmentFile=/etc/ocmEnv.conf

b/ Uncomment and point the settings to the environment file containing the environment variables. For example:

EnvironmentFile=/etc/ocmEnv.conf

4/ Please include the environment variables that the OPSWAT Central Management service should use in the content of the environment file. Below is an example of the environment file:

#system proxy setting, optional
http_proxy=proxy:3128

5/ Reload OPSWAT Central Management service for the modification to take effect.

sudo systemctl daemon-reload

6/ Start OPSWAT Central Central Management: **sudo systemctl start ocm**

Info

In case of startup problems, please refer to the startup log in /var/log/ocm or systemd log.

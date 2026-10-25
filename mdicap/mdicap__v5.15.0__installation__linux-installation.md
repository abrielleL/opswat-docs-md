<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/installation/linux-installation -->

# Linux Deployment

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Preliminary notes](/docs/mdicap/v5.15.0/installation/linux-installation#preliminary-notes)

If the MetaDefender ICAP Server package dependencies are not installed on your system you may need to have a working Internet connection or you may have to provide the Installation media during the installation. Consult your Operating System documentation on how to use Installation media as a package repository.

## [Package installers](/docs/mdicap/v5.15.0/installation/linux-installation#package-installers)

### [Ubuntu or Debian installs](/docs/mdicap/v5.15.0/installation/linux-installation#ubuntu-or-debian-installs)

1. Download *mdicapsrv* package from the [OPSWAT Portal](https://portal.opswat.com). Make sure that you download the applicable package for your distribution
2. Upload the installation package to your server computers
3. Install the product with the following command (<filename> is the MetaDefender ICAP Server package you downloaded from our portal):

$ sudo dpkg -i <filename>

4. If dpkg shows error messages about missing dependencies you should execute:

$ sudo apt-get install -f

5. Open a web browser and point to (<server name or IP> is the DNS name or IP address of your server):

http://<server name or IP>:8048
### [Red Hat Enterprise Linux or CentOS installs](/docs/mdicap/v5.15.0/installation/linux-installation#red-hat-enterprise-linux-or-centos-installs)

1. Download *mdicapsrv* package from the [OPSWAT Portal](https://portal.opswat.com). Make sure that you download the applicable package for your distribution
2. Upload the installation package to your server computers
3. Install the product with the following command (<filename> is the MetaDefender ICAP Server package you downloaded from our portal):

$ sudo yum install <filename>

4. Open a web browser and point to (<server name or IP> is the DNS name or IP address of your server):

http://<server name or IP>:8048

5. Enter default login credentials, username: **admin**, password: **admin**

## [Initialization](/docs/mdicap/v5.15.0/installation/linux-installation#initialization)

### [Without Ignition file](/docs/mdicap/v5.15.0/installation/linux-installation#without-ignition-file)

Info

The installation on Linux environment will ask to input the required information from console incase the ignition file does not exist in designated location

The installation will request user input Postgres server information via **console**. User can provide information or hit enter to select default value in []

Postgres server information request:

- DATABASE MODE (default is standalone mode)

  - 1: for standalone
  - 4: for share mode
- Type of database (default is local)

  - local
  - remote
- Port (default is 5433)
- Database username: postgres
- Database password

**For example:** Here is the screenshot if user input PostgreSQL information as below:

- database mode: standalone
- type of database: local
- port: 5434
- database username: postgres

JsonCopyRunning transaction check
Running transaction test
Transaction test succeeded
Running transaction
===========
Please input your postgres server information...
You can enter to make default value in [] for each option
===========
DATABASE MODE must be (1-standalone mode or 4-share mode) [1]: 1
TYPE (local or remote) [local]: local
PORT [5433]: 5434
USER [postgres]: postgres
PASSWORD:
CONFIRM PASSWORD:
Complete creating /etc/opswat/mdicapsrv.conf.
### [With Ignition file](/docs/mdicap/v5.15.0/installation/linux-installation#with-ignition-file)

Info

Linux can use ignition file to add PostgreSQL server information since MD ICAP Server 5.2.0 , refer to [Deployment automation support](/docs/mdicap/v5.15.0/installation/deployment-automation-supporthhj)

Make sure to create the ignition file before you go ahead and install MetaDefender ICAP Server

- **Linux:**`/etc/opswat/mdicapsrv.conf`

<!-- source: https://www.opswat.com/docs/supply-chain/installation/upgrading-from-a-previous-version -->

# Upgrading from a previous version

## [Upgrading from a previous version on Unix-based deployments](https://docs.opswat.com/mdss/installation/upgrading-from-a-previous-version#upgrading-from-a-previous-version-on-unix-based-deployments)

### Preliminary notes

Upgrading is usually a two-step process:

1. upgrade the *mdssc* package by installing the newer package
2. upgrade the existing code by downloading new images

### Acquire the installer package

In order to acquire the new package please visit My OPSWAT -> [Product Downloads](https://my.opswat.com/home/metadefender-software-supply-chain)

> **Warning**
>
> Installing the new package removes all MetaDefender Software Supply Chain containers and images from the machine. Named volumes (database data) and `/etc/mdssc/customer.env` are preserved. On an offline machine, stage the offline toolkit archive before you install the package.

### Debian / Ubuntu package (.deb)

1. Back up before upgrading

```bash
sudo mdssc -u export_db      # writes /etc/mdssc/db_<...>.tar
sudo mdssc -u export_settings
```

2. Update packages (online installations only)

```bash
sudo apt-get update
```

3. Move to the folder containing the installer and install it

```bash
sudo dpkg -i <name of the file>.deb || sudo apt-get install -f
```

For an offline installation, use the following form instead:

```bash
sudo dpkg -i ./mdssc-<VERSION>.deb
```

4. Update images (online installations only) — this pulls images from the container registry. For offline installations, see "Offline (air-gapped) upgrade" below.

```bash
sudo mdssc -u update
```

5. Optionally, you can check the status using the following command:

```bash
sudo mdssc -c status
```

6. Open a browser and navigate to the web interface: http://<server> to configure your deployment

### Red Hat Enterprise Linux / CentOS package (.rpm)

1. Back up before upgrading

```bash
sudo mdssc -u export_db      # writes /etc/mdssc/db_<...>.tar
sudo mdssc -u export_settings
```

2. Update packages (online installations only)

```bash
sudo yum -y update
```

3. Move to the folder containing the installer and install it

```bash
sudo yum upgrade <name of the file>.rpm
```

4. Update images (online installations only) — this pulls images from the container registry. For offline installations, see "Offline (air-gapped) upgrade" below.

```bash
sudo mdssc -u update
```

5. Optionally, you can check the status using the following command:

```bash
sudo mdssc -c status
```

6. Open a browser and navigate to the web interface: http://<server> to configure your deployment

### Offline (air-gapped) upgrade

Before you begin, transfer **both** files to the offline machine: the release RPM and the offline toolkit archive of the **same version**. Extract the toolkit before installing the RPM — installing the RPM removes the currently installed containers and images, and without the toolkit already on disk there is nothing left to start.

```bash
tar -xzf mdssc-offline-<VERSION>.tar.gz
sudo yum upgrade -y --disablerepo="*" ./mdssc-<VERSION>.noarch.rpm
cd mdssc-offline-<VERSION>
sudo ./mdssc.sh -u load_images
sudo mdssc -c start
sudo mdssc -c status
```

Do not run `sudo yum -y update` or `sudo mdssc -u update` on an offline machine — both require internet access.

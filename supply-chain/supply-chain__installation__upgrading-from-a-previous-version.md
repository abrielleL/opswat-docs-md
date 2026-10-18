<!-- source: https://www.opswat.com/docs/supply-chain/installation/upgrading-from-a-previous-version -->

# Upgrading from a previous version

## [Upgrading from a previous version on Unix-based deployments](https://docs.opswat.com/mdss/installation/upgrading-from-a-previous-version#upgrading-from-a-previous-version-on-unix-based-deployments)

### Preliminary notes

Upgrading is usually a two-step process:

1. upgrade the *mdssc* package by installing the newer package
2. upgrade the existing code by downloading new images

### Notes for upgrading to 4.1 and later

When upgrading from 4.0.x behind a TLS-terminating load balancer, set [ALLOWED_ORIGINS](https://www.opswat.com/docs/supply-chain/configuration/custom-configuration#allowed-origins). Otherwise, the Cross Domain Transfer Activity Log stops loading.

### Acquire the installer package

In order to acquire the new package please visit My OPSWAT -> [Product Downloads](https://my.opswat.com/home/metadefender-software-supply-chain)

### Debian / Ubuntu package (.deb)

1. Update your packages

```bash
sudo apt-get update
```

2. Move to the folder containing the installer and install it

```bash
sudo dpkg -i <name of the file>.deb || sudo apt-get install -f
```

3. Start the service

```bash
sudo mdssc -u update
```

4. Optionally, you can check the status using the following command:

```bash
sudo mdssc -c status
```

5. Open a browser and navigate to the web interface: http://<server> to configure your deployment

### Red Hat Enterprise Linux / CentOS package (.rpm)

1. Update your packages

```bash
sudo yum -y update
```

2. Move to the folder containing the installer and install it

```bash
sudo yum upgrade <name of the file>.rpm
```

> **Warning**
>
> If `yum` fails with `Cannot download repomd.xml`, run the upgrade with all repositories disabled:
>
> ```bash
> sudo yum upgrade -y --disablerepo="*" ./mdssc-<version>.noarch.rpm
> ```

3. Start the service

```bash
sudo mdssc -u update
```

4. Optionally, you can check the status using the following command:

```bash
sudo mdssc -c status
```

5. Open a browser and navigate to the web interface: http://<server> to configure your deployment

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)

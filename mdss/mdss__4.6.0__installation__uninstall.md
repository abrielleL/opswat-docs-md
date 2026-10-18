<!-- source: https://www.opswat.com/docs/mdss/4.6.0/installation/uninstall -->

# Uninstall

> **NOTE**
>
> > If the current MetaDefender Storage Security (MDSS) deployment (4.0.0 or later) was upgraded from 3.6.1 or earlier, any existing MongoDB backups will be deleted during uninstallation. Manually back up the data beforehand if it’s still needed.

## Uninstall via Command Line

## **Debian / Ubuntu (.deb package)**

To remove all files installed by MetaDefender Storage Security:

```bash
sudo mdss -u clean
```

To remove the `mdss` package from the system:

```bash
sudo apt-get remove mdss
```

## **Red Hat Enterprise Linux / CentOS (.rpm package)**

To remove all files installed by MetaDefender Storage Security

```bash
sudo mdss -u clean
```

To remove the `mdss` package from the system:

```bash
sudo yum remove mdss
```

## Uninstall via Uninstall Wizard (Windows only)

> **NOTE**
>
> > The Uninstall Wizard is available only for the Windows installer (`.msi`).

## Step-by-Step Instructions

1. Open **Start** → **Control Panel** → **Uninstall a program**
2. Locate **MetaDefender Storage Security** in the list
3. Double-click the entry
4. Click **Uninstall and Yes** to begin the process

![](https://uploads.developerhub.io/prod/k8zL/rwpqhhe2j51egtj8nv5245cv9e2glds7mdppn44xwj4cmecp47udh63abjd93vtw.png)

5. Wait for the uninstallation to complete
6. Click **Finish** to finish.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

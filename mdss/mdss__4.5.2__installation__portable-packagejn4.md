<!-- source: https://www.opswat.com/docs/mdss/4.5.2/installation/portable-packagejn4 -->

# Portable Package

This guide provides instructions on how to deploy MetaDefender Storage Security docker images without using the the installer. This method is intended for deployment scenarios where installing docker and docker-compose is not possible using official installation methods.

> **Info**
>
> It's recommended to have the same dependencies as the ones required for the [offline installation](https://www.opswat.com/docs/mdss/installation/linux-offline-installation#installing-binary-packages) preinstalled on the target host machine.

## Downloading the portable toolkit

The toolkit is available on the **MyOPSWAT** portal under **MetaDefender Storage Security** in the **MetaDefender Storage Security Portable Toolkit** section. The package needs to be extracted to the desired path on the target machine and the following steps should all be performed from the same path where the package is extracted on the target machine.

#### Starting MetaDefender Storage Security

From the path where the portable package is extracted, MDSS can be started using the regular startup command but specifying the local path to the `mdss.sh` script:

```bash
sudo ./mdss.sh -c start
```

Using this method, all mdss commands (start, stop etc.) will need to be executed from the same path where the package is extracted.

> **Info**
>
> When running in portable mode, the `mdss.sh` script detects if docker is already installed or if the bundled docker binaries should be used in which case the following should be taken into consideration:
>
> - Docker commands will not work from the command line by default unless using the docker binarys directly from the bundled `docker` folder.
> - The bundled docker binary is not running as a service, the `dockerd` process is started automatically when running `mdss` commands.
> - Since docker is not running as a service it does not automatically start at boot

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

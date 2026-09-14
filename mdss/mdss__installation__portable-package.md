<!-- source: https://www.opswat.com/docs/mdss/installation/portable-package -->

# Portable Package

This guide provides instructions on how to deploy MetaDefender Storage Security docker images without using the the installer. This method is intended for deployment scenarios where installing docker and docker-compose is not possible using official installation methods.

Info

It's recommended to have the same dependencies as the ones required for the [offline installation](/docs/mdss/installation/linux-offline-installation#installing-binary-packages) preinstalled on the target host machine.

## [Downloading the portable toolkit](/docs/mdss/installation/portable-package#downloading-the-portable-toolkit)

The toolkit is available on the **MyOPSWAT** portal under **MetaDefender Storage Security** in the **MetaDefender Storage Security Portable Toolkit** section. The package needs to be extracted to the desired path on the target machine and the following steps should all be performed from the same path where the package is extracted on the target machine.

#### [Starting MetaDefender Storage Security](/docs/mdss/installation/portable-package#starting-metadefender-storage-security)

From the path where the portable package is extracted, MDSS can be started using the regular startup command but specifying the local path to the `mdss.sh` script:

BashCopysudo ./mdss.sh -c start

Using this method, all mdss commands (start, stop etc.) will need to be executed from the same path where the package is extracted.

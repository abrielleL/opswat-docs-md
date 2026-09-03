<!-- source: https://www.opswat.com/docs/mddownloader/v3.4.0/installation/installing-update-downloader -->

# Installing Update Downloader

Before starting the installation please make sure your test computer or virtual machine meets the [minimum hardware and software requirements](/installation/before-installation).

## Installing Update Downloader on Ubuntu or Debian computers

1. Visit the [My OPSWAT](https://my.opswat.com/). Search for MetaDefender Core, navigate to section "Modules & Utilities", then you can find the product at "Update Downloader for Offline Environment".
2. Make sure that you download the applicable package for Debian 12 / Ubuntu 22.04.
3. Upload the installation package to your test computers.
4. Install the product with sudo dpkg -i <filename>, where filename is the Update Downloader package you downloaded from our portal.
5. If dpkg shows error messages about missing dependencies you should execute sudo apt-get install -f
6. Open a web browser and point to http://<server name or IP>:8028
7. Follow welcome wizard to create local admin user account and start working on Update Downloader

## Installing Update Downloader on Red Hat Enterprise or Rocky Linux computers

1. Visit the [My OPSWAT](https://my.opswat.com/). Search for MetaDefender Core, navigate to section "Modules & Utilities", then you can find the product at "Update Downloader for Offline Environment".
2. Make sure that you download the applicable package for Red Hat Enterprise Linux or Rocky Linux.
3. Upload the installation package to your test computers
4. Install the product with sudo yum install <filename>, where filename is the Update Downloader package you downloaded from our portal
5. Open a web browser and point to http://<server name or IP>:8028
6. Follow welcome wizard to create local admin user account and start working on Update Downloader

## Installing Update Downloader on Windows

1. Visit the [My OPSWAT](https://my.opswat.com/). Search for MetaDefender Core, navigate to section "Modules & Utilities", then you can find the product at "Update Downloader for Offline Environment".
2. Make sure that you download the applicable package for Windows Server 2022.
3. Upload the installation package to your test computers
4. Install the product with executing the installer
5. Open a web browser and point to http://<server name or IP>:8028
6. Follow welcome wizard to create local admin user account and start working on Update Downloader

To continue the basic setup, follow the license activation instructions on [Step 2. License activation](/installation/license-activation)

For more information on Installation procedures see [Installing Update Downloader](/installation/installing-update-downloader)

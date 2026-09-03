<!-- source: https://www.opswat.com/docs/mddownloader/v3.4.0/installation/installing-update-downloader-using-the-command-line -->

# Installing Update Downloader using the Command Line

## [Preliminary notes](/docs/mddownloader/v3.4.0/installation/installing-update-downloader-using-the-command-line#preliminary-notes)

- If the Update Downloader package dependencies are not installed on your system you may need to have a working Internet connection or you may have to provide the Installation media during the installation. Consult your Operating System documentation on how to use Installation media as a package repository.

## [Debian package (.deb)](/docs/mddownloader/v3.4.0/installation/installing-update-downloader-using-the-command-line#debian-package-deb)

install cmdCopysudo dpkg -i <file name> || sudo apt-get install -f
## [On Red Hat Enterprise Linux / CentOS package (.rpm)](/docs/mddownloader/v3.4.0/installation/installing-update-downloader-using-the-command-line#on-red-hat-enterprise-linux--centos-package-rpm)

install cmdCopysudo yum install <file name>
## [Windows package (.msi)](/docs/mddownloader/v3.4.0/installation/installing-update-downloader-using-the-command-line#windows-package-msi)

On Windows systems it is possible to install the product by running the corresponding .msi file.

From command line interface it is also possible to install the product by executing

install cmdCopymsiexec /i <msi file name> <option key>=<option value>

where the possible keys and their default values are the following:

| Key | Default Value | Description |
| --- | --- | --- |
| RESTADDRESS | 0.0.0.0 | REST interface binding address |
| RESTPORT | 8028 | REST interface binding port |

For details on using msiexec please consult [Windows installer documentation](https://technet.microsoft.com/en-us/library/cc782896%28v=ws.10%29.aspx).

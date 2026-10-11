<!-- source: https://www.opswat.com/docs/mdicap/troubleshooting/how-to-create-support-package -->

# How to create support package

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info

A support package contains essential information regarding the operating system and OPSWAT software found on the machine.

Warning - Security and Privacy Concerns

The contents of the generated package may contain sensitive information that may require special handling.

## [Linux](/docs/mdicap/troubleshooting/how-to-create-support-package#linux)

To create a package you must start the script found under **/usr/bin/mdicapsrv-collect-support-data.sh**.

As the script processes the necessary information, the script generates the support package output.

The package files is a tar.gz archive with the following name:

mdicapsrv-<VERSION>-support-<TIMESTAMP>.tar.gz

Where the timestamp is the date when the package was generated.

Example:

mdicapsrv-4.2.0-support-1439983514.tar.gz

The generated package will be placed in the same location as the script that was called.

## [Windows](/docs/mdicap/troubleshooting/how-to-create-support-package#windows)

To create a package you must start the script found under the installation directory of the product, default this is **C:\Program Files\Metadefender ICAP Server\mdicapsrv-collect-support-data.bat**.

As the script processes the necessary information, the script generates the support package output.

The package files is a zip archive with the following name:

mdicapsrv-<VERSION>-support-<TIMESTAMP>.zip

Where the timestamp is the date when the package was generated.

Example:

mdicapsrv-4.2.0-support-1439983514.zip

The generated package will be placed in the same location as the script that was called.

## [Content of the created package](/docs/mdicap/troubleshooting/how-to-create-support-package#content-of-the-created-package)

The support package contains the following elements:

| Relative path | Type | Description |
| --- | --- | --- |
| config | directory | The configuration files of OPSWAT software found on the machine |
| config/config.copy | file (binary) | Config database **without** user data |
| log | directory | The log files of OPSWAT software found on the machine |
| os.info | file (text) | Operating system information |
| hw.info | file (text) | Hardware information |
| network.info | file (text) | Network information |
| files.info | file (text) | OPSWAT software directory information |

Note

You are recommended to check the content of the generated package to make sure it does not contain any confidential information.

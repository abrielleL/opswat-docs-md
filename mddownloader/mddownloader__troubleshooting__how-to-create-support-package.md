<!-- source: https://www.opswat.com/docs/mddownloader/troubleshooting/how-to-create-support-package -->

# How to create support package

A support package contains essential information regarding the operating system and OPSWAT software found on the machine.

## Linux

To create a package you must start the script found under **/usr/bin/ometadownloader-collect-support-data.sh**.

As the script processes the necessary information, the script generates the support package output.

The package files is a tar.gz archive with the following name:

packageCopyometadownloader-support-<TIMESTAMP>.tar.gz

Where the timestamp is the date when the package was generated.

Example:

packageCopyometadownloader-support-1439983514.tar.gz

The generated package will be placed in the same location as the script that was called.

## Windows

To create a package you must start the script found under the installation directory of the product, default this is **C:\Program Files\Metadefender Update Downloader\ometadownloader-collect-support-data.bat**.

As the script processes the necessary information, the script generates the support package output.

The package files is a zip archive with the following name:

packageCopyometadownloader-support-<TIMESTAMP>.zip

Where the timestamp is the date when the package was generated.

Example:

packageCopyometadownloader-support-1439983514.zip

The generated package will be placed in the same location as the script that was called.

## Content of the created package

The support package contains the following elements:

- **configuration** : the configuration files of OPSWAT software found on machine
- **log** : the log files of OPSWAT software found on machine
- **system information** : system information stored in file named os.info
- **hardware information:** hardware information stored in file named hw.info
- **network information:** network information stored in file named network.info
- **directory information:** OPSWAT software directory information stored in file named files.info
- **copy of config database** : config database **WITHOUT** user data

You can check the content of the generated package to make sure it does not contain any confidential information.

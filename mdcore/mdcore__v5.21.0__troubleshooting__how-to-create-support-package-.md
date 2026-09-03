<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package- -->

# How to Create Support Package With Bundle Tools?

A support package contains essential information regarding the operating system and OPSWAT software found on the machine.

#Windows
ometascan-collect-support-data.bat
#Linux
ometascan-collect-support-data.sh

**Parameters (optional):**

#### [-max-log N](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-#-max-log-n)

- Define a number of log files to be gathered and added into support package.
- The tool sorts log files by Date Modified with descending order.
- If not set, or set 0, or set a negative number, the tool will ignore it and collect all log files.

Warning

The `-max-log` parameter is calculated based on the number of log files, not the number of days. Since MetaDefender Core can generate multiple log files in a single day, please ensure that the calculation accurately reflects the total number of log files.

#### [-enable-redact 1|0](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-#-enable-redact-10)

- Hide sensitive information in the support package.
- 1 is enable, 0 is disable. The default is 0 and will not redact sensitive information.
- The information will be redact: IP address, MAC, file path.

#### [-start-date and -end-date](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-#-start-date-and--end-date)

These 2 options will accept either *Epoch timestamp (in seconds)* or *ISO 8061 date format* `YYYY-MM-DD` with local time zone.

Example:

- Epoch timestamp (second) format `ometascan-collect-support-data.bat -start-date 1773766800 -end-date 1773853200`
- ISO 8061 timestamp format `ometascan-collect-support-data.bat -start-date 2026-03-18 -end-date 2026-03-19` -> collect logs from *2026-03-18 00:00:00* to *2026-03-19 00:00:00 (UTC+7:00)* Note: We support this format to make our script easier to use for CX / customer.

#### [-lite](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-#-lite)

Use this option when users want to create a lightweight support package, reduce size and generation time. When use this option, users do not need to care about other options.

For example (Linux)

BashCopy/usr/bin/ometascan-collect-support-data.sh -lite
## [Creating the package on Linux](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-#creating-the-package-on-linux)

Run **/usr/bin/ometascan-collect-support-data.sh**

As the script processes the necessary information, the script generates the support package output.

The package files are tar.gz archive with the following name:

ometascan-<VERSION>-support-<TIMESTAMP>.tar.gz

Where the timestamp is the date when the package was generated.

Example:

ometascan-5.14.1-1-support-1439983514.tar.gz

The generated package will be placed in the current working directory.

## [Creating the package on Windows](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-#creating-the-package-on-windows)

Run script found under the installation directory of the product, default is **C:\Program Files\OPSWAT\Metadefender Core\ometascan-collect-support-data.bat**

As the script processes the necessary information, the script generates the support package output.

The package files is a zip archive with the following name:

ometascan-<VERSION>-support-<TIMESTAMP>.zip

Where the timestamp is the date when the package was generated.

Example:

ometascan-5.14.1-1-support-1439983514.zip

The generated package will be placed in the same location as the script that was called.

Info

If the support package too big in size, we can also input -max-log N for to collect logs for last N logs. For example

**ometascan-collect-support-data.bat -max-log 15**

Will collect logs for last 15 newest logs.

## [Support Package contents](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-#support-package-contents)

The support package contains the following elements:

- **configuration** : the configuration files of OPSWAT software found on machine
- **log** : the log files of OPSWAT software found on machine
- **system information** : system information stored in file named os.info
- **hardware information:** hardware information stored in file named hw.info
- **network information:** network information stored in file named network.info
- **directory information:** OPSWAT software directory information stored in file named files.info
- **copy of config database** : config database **WITHOUT** user data

You can check the content of the generated package to make sure it does not contain any confidential information.

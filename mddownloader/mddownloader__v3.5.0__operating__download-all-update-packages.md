<!-- source: https://www.opswat.com/docs/mddownloader/v3.5.0/operating/download-all-update-packages -->

# Download all update packages

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Goto Inventory > Products > Select the product you want to download

Hitting **Download All As Zip** button at the top right to download all engines' update packages as single archive .zip file

Confirm the package generation and wait for the package to be built.

When package generation is done the modal looks as below. For security reasons the modal also shows the SHA256 checksum of the generated package file so it can be validated.

The resulting zip file among the update packages (**.yml and .zip files**) will contain a file called **report.txt** that holds information on the package generation and looks like the following.

report.txtCopy===== Update package report =====
Created at 2018-06-07T07:06:01.879Z
 
There are 20 update packages in this archive
 
== clamav_1_windows-engine ==
 
clamav_1_windows-engine-1486651156-1528354018032.yml
Package version: 0.99.2-24
Filesize: 5565 bytes
SHA256: 4091a5d032c8f2996a362fa266f56a4cf9fd949acb15d33ce4edfc9caa6b72d0
OPSWAT digital signature.......... VALIDATED
Checksum.......................... VALIDATED
clamav_1_windows-engine-1486651156.zip
Filesize: 4134048 bytes
SHA256: fcaaf883823dec041c540236d0a4b76496e4a088e0a21ebbefe12bf0fdfe432c
Extraction........................ VALIDATED
Checksum of the extracted files... VALIDATED
 
== 7z_4_linux-database ==
 
7z_4_linux-database-1507797673-1528354018032.yml
Package version: 16.02-242
Filesize: 1578 bytes
SHA256: 29acddc32b8b3656df89466bf46c6770b1dfe881d5982b007f8c8c97805515e4
OPSWAT digital signature.......... VALIDATED
Checksum.......................... VALIDATED
7z_4_linux-database-1507797673.zip
Filesize: 929419 bytes
SHA256: e3b7f772d99837c8fdd19e619013af7f5d60bc7c4accf982afa1a90a06f1fe8b
Extraction........................ VALIDATED
Checksum of the extracted files... VALIDATED
 
== eset_1_windows_engine ==
...

If something goes wrong during the package generation the zip won't be available and an error message will be displayed.

Info

**Note:**

- Generated package contains all those update packages which states are "ready". The "exporting" state means that the update package export is still in progress and it will not be contained by the generated package.
- Depending on the number of update packages, the generated package can be a huge zip file.
- Before the package generation, the product checks if there is enough free disk space and in case of insufficient space, it informs you on the needed amount.
- After a successful download the generated package will be removed to free up disk space.
- When a new package is generated all previous ones that are not currently being downloaded will be removed automatically.

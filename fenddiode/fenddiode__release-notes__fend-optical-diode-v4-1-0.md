<!-- source: https://www.opswat.com/docs/fenddiode/release-notes/fend-optical-diode-v4-1-0 -->

# Fend Optical Diode v4.1.0

Released: 05/28/2024

## [Features/Changes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-1-0#featureschanges)

1. Added SFTP client/server support
2. Added support for implicit FTPS (Port 990)
3. Added URL support to the output side FTP/FTPS client
4. Added a new option for FTP/FTPS change directory handling to better accommodate Linux and Windows platform differences. *NOTE: If you are currently using Linux with FTP and are using absolute paths, after upgrading to 4.1.0 you will need to uncheck "Relative Pathing Enabled" under the output side FTP settings to continue with the current behavior. See user's manual for specifics.
5. Streamlined how FTP/FTPS server verification works. Removed the "Enable server verification" option from output side FTP/FTPS/SFTP client configurations. Now only verifies if a server certificate is present in the configuration. To disable server verification, clear the server certificate.
6. Added configurable FTP/FTPS client timeouts
7. Improved FTP/FTPS diagnostic messages
8. Added support for TLS to input side TCP Server. End to end TLS now available
9. Removed unused configuration fields from FTP/FTPS tabs in the configuration tool. General interface improvements

## [Fixes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-1-0#fixes)

1. Improved the speed of and added visual indicators to the configuration login process
2. Fixed an issue where the configuration interface could get stuck loading a backup file
3. Fixed an issue where the configuration interface could get stuck loading if a network error occurred
4. Fixed an issue with clearing certificates from the FTPS and TLS certificate fields once entered

<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/troubleshooting/pin-code-reset-tool -->

# PIN Code Reset Tool

## [Overview](/docs/mdcore/v5.21.0/troubleshooting/pin-code-reset-tool#overview)

The `ometascan-reset-pin-code` utility is a command-line tool designed to manage PIN codes for OPSWAT MetaDefender Core database configuration. This tool allows administrators to either remove existing PIN code or configure new one for database access security.

## [Purpose](/docs/mdcore/v5.21.0/troubleshooting/pin-code-reset-tool#purpose)

This tool manages the PIN code protection for database credentials in MetaDefender Core. The PIN code is stored in encrypted database credential files and provides an additional layer of security for database access.

## [Usage](/docs/mdcore/v5.21.0/troubleshooting/pin-code-reset-tool#usage)

**Windows**

BashCopy# Goto installation folder, for example
cd c:\Program Files\OPSWAT\MetaDefender Core\
#Run the tool
ometascan-reset-pin-code.exe

**Linux**

BashCopy/usr/sbin/ometascan-reset-pin-code

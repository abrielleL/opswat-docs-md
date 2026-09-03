<!-- source: https://www.opswat.com/docs/netwall/knowledge-bases/what-are-the-minimum-number-of-connections-available-required-fo -->

# What are the minimum number of connections available required for FTP files transfer in MetaDefender Security Gateway appliance?

This article applies to all versions of versions of MetaDefender Security Gateway.

## [Problem:](/docs/netwall/knowledge-bases/what-are-the-minimum-number-of-connections-available-required-fo#problem)

Certain environments may restrict FTP traffic down to 1 connection allowed at the time from the server. This can cause issues when file transfer is enabled. With one connection configured, the Test button in the product would be able to list/check the files in the folder, but the transfer would not work.

## [Background:](/docs/netwall/knowledge-bases/what-are-the-minimum-number-of-connections-available-required-fo#background)

A FTP Client normally uses 2 connections to transfer files:

- A **Control Connection** that is used for sending commands and receiving responses from the FTP Server
- A **Data Connection** that is used for transferring files between the client and the server

## [Solution:](/docs/netwall/knowledge-bases/what-are-the-minimum-number-of-connections-available-required-fo#solution)

The MetaDefender Security Gateway Appliance needs at minimum 2 connections available for FTP file transfer to work properly.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/support).

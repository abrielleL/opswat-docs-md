<!-- source: https://www.opswat.com/docs/fenddiode/release-notes/fend-optical-diode-v4-2-1 -->

# Fend Optical Diode v4.2.1

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Released: 10/11/2024

## [Features/Changes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-2-1#featureschanges)

1. Added support for the following TLS encryption algorithms for client and server

   1. ec/ecdsa384
   2. ec/ecdsa521
2. Added support for the following SSH encryption algorithms for client and server

   1. host key: ed25519
   2. public key auth: rsa1024 to 4096
3. Expanded TLS and SFTP support for more Linux clients/servers

## [Fixes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-2-1#fixes)

1. Fixed an issue where the Modbus starting address + read count could exceed 65535
2. Fixed an issue where having multiple Modbus RTU master/clients on a Modbus serial network could cause the diode to require a reset.
3. Fixed an issue that would cause the diode to fail to connect to certain versions of WinSCP
4. Fixed an issue that would cause the diode to fail to reconnect for an extended period of time when encountering an error uploading when using cellular MQTT
5. Fixed an issue where an incorrect Modbus total register count would be displayed after a factory reset or restore from backup during the first login

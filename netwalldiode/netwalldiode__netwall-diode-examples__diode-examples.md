<!-- source: https://www.opswat.com/docs/netwalldiode/netwall-diode-examples/diode-examples -->

# MetaDefender Optical Diode Examples

This appendix shows examples of unidirectional file transfer and streaming processes and a bilateral streaming process.

## [File Transfer](/docs/netwalldiode/netwall-diode-examples/diode-examples#file-transfer)

After you configure MetaDefender Optical Diode (hereinafter Optical Diode) BLUE and RED and the transfer parameters, files placed in a specified location on a customer provided server in the BLUE zone transfer automatically to a specified location on a server in the RED zone.

Optical Diode BLUE monitors the specified location on the customer server in the BLUE zone for new files. When a new file is detected, Optical Diode BLUE monitors that file until it is considered accessible (i.e., no longer being written to), then reads the file and transfers the data to Optical Diode RED.

Optical Diode RED transfers the file to the specified location on the customer server in the RED zone. After a file is transferred, the Optical Diode removes it from its original location.

This example shows a general file transfer flow. While FTP is shown, the flow applies to Windows File Share as well.

The example configures Optical Diode BLUE to monitor a customer-owned FTP server in the BLUE zone and Optical Diode RED to transfer the data to a customer-owned FTP server in the RED zone.

Optical Diode BLUE configuration:

- Enabled: (checked)
- FTP User: blueuser
- FTP Password/Re-enter Password: bluepassword
- FTP Server: 192.168.100.10
- FTP Share: blue_ftp

Optical Diode RED configuration (example values given):

- Enabled: (checked)
- FTP User: reduser
- FTP Password/Re-enter Password: redpassword
- FTP Server: 192.168.100.125
- FTP Share: red_ftp

The following sequence occurs when a file is transferred from the BLUE zone to the RED zone:

1. Optical Diode BLUE (192.168.100.120) monitors the location on the BLUE zone FTP server (192.168.100.10) specified in FTP Share.
2. When Optical Diode BLUE detects a file, it monitors the file until is it no longer being written to.

   1. Optical Diode BLUE downloads the file, using FTP, transfers the file to Optical Diode RED (192.168.50.75), and deletes the file from its original location on the BLUE zone FTP server.
   2. Optical Diode RED initiates an FTP connection to the RED zone FTP server (192.168.50.125).
   3. Optical Diode RED uploads the file to the RED zone FTP server.

## [Unidirectional Streaming](/docs/netwalldiode/netwall-diode-examples/diode-examples#unidirectional-streaming)

Streaming is used to transfer UDP (unicast and multicast) or TCP data from the BLUE zone to the RED zone.

The following example shows TCP streaming for a syslog.

This example configures a UNIX machine in the BLUE zone to send syslog data to a UNIX machine in the RED zone.

The TCP Streaming Configuration for MetaDefender Optical Diode:

- Source IP: 192.168.100.11
- Destination IP: 192.168.50.25
- Source Port: 514
- Destination Port: 514
- Type: TCP Unilateral
- Max Sessions: 1
- Description: Syslog to server in RED zone

This configuration allows the BLUE zone UNIX machine to establish a session with the UNIX machine in the RED zone, both using port 514.

The BLUE zone UNIX machine uses the Optical Diode BLUE IP address (192.168.100.120) as the address of the RED zone UNIX machine.

The following sequence occurs when a BLUE zone UNIX machine attempts to send a syslog to the RED zone UNIX machine:

1. Optical Diode BLUE (192.168.100.120) listens for connections on 514. When it receives the TCP request, it identifies the IP address of the BLUE zone UNIX machine (192.168.100.11). If that IP address was not listed as a Source IP, the connection is dropped and a message is logged to Syslog.

   1. Optical Diode BLUE assigns a unique identifier (UUID) to this connection instance and sends a connect request to MetaDefender Optical Diode RED (192.168.50.75).
   2. Optical Diode RED receives the connect request and tries to open a TCP connection with the RED zone UNIX machine (192.168.50.25).
   3. Optical Diode BLUE receives the connection status.

      - If the connection status is failed, the connection between Optical Diode BLUE and the BLUE zone UNIX machine is dropped.
      - If the connection status is good, the syslog data from the BLUE zone UNIX machine is sent to Optical Diode RED, using the UUID as a reference.
   4. Optical Diode RED receives the syslog data and sends it to the RED zone UNIX machine.
   5. If the connection between Optical Diode RED and the RED zone UNIX machine fails Optical Diode RED drops the connection with the UNIX machine.
   6. Optical Diode BLUE reads the connection status from Optical Diode RED and drops its connection with the BLUE zone UNIX machine if the connection status is failed.
   7. If the connection between Optical Diode BLUE and the BLUE zone UNIX machine fails, or if the UNIX machine closes the connection gracefully, Optical Diode BLUE sends a close request to Optical Diode RED.
   8. Optical Diode RED terminates its connection with the RED zone UNIX machine.

MetaDefender

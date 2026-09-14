<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-test-the-syslog-server-functionality-from-metadefender-co -->

# How to Test the Syslog Server functionality from MetaDefender Core?

## [Windows](/docs/mdcore/knowledge-base/how-to-test-the-syslog-server-functionality-from-metadefender-co#windows)

Execute this in PowerShell.

**UDP Syslog**

PowershellCopy$syslogServer = "<syslog_server_ip>"
$syslogPort = 514
$message = "<34>Test Syslog message"
$udpClient = New-Object System.Net.Sockets.UdpClient
$udpClient.Connect($syslogServer, $syslogPort)
$encodedMessage = [System.Text.Encoding]::ASCII.GetBytes($message)
$udpClient.Send($encodedMessage, $encodedMessage.Length)
$udpClient.Close()
Write-Output "Syslog message sent."

**TCP Syslog**

PowershellCopy$syslogServer = "<syslog_server_ip>"
$syslogPort = 601
$message = "<34>Test Syslog message`n"
$tcpClient = New-Object System.Net.Sockets.TcpClient($syslogServer, $syslogPort)
$stream = $tcpClient.GetStream()
$writer = New-Object System.IO.StreamWriter($stream)
$writer.WriteLine($message)
$writer.Flush()
$writer.Close()
$stream.Close()
$tcpClient.Close()
Write-Output "Syslog message sent."
## [Linux](/docs/mdcore/knowledge-base/how-to-test-the-syslog-server-functionality-from-metadefender-co#linux)

Using the Linux command below.

**UDP Syslog**

BashCopyecho "<34>Test Syslog message" | nc -u -w1 <syslog_server_ip> 514

**TCP Syslog**

BashCopyecho "<34>Test Syslog message" | nc <syslog_server_ip> 601Info

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).

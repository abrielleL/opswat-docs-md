<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-to-send-a-file-to-icap-server-for-testing-the-functionalites -->

# How to send a file to ICAP server for testing the functionalities using the powershell script?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender ICAP Server releases deployed on Windows systems.

The script shown below is made to specifically work with text files only (using the .txt format). Using different files formats will result in the script failing.

#### [Create a powershell script with the content below and save it as icap_win.ps1](/docs/mdicap/v5.15.0/knowledge-base/how-to-send-a-file-to-icap-server-for-testing-the-functionalites#create-a-powershell-script-with-the-content-below-and-save-it-as-icap_winps1)

TEXTCopyparam (
[string]$icapServer = "127.0.0.1", #ICAP server IP
[int]$icapPort ="1344", # ICAP default port
[string]$icapService = "/OMSScanReq-AV", # ICAP service name
[string]$filePath = "" # Path to the file
)
# Read file content
$fileContent = [System.IO.File]::ReadAllBytes($filePath)
$fileSize = $fileContent.Length
$chunkSize = [Convert]::ToString($fileSize, 16) # Convert size to hexadecimal
# Define ICAP Headers
$icapRequest = "REQMOD icap://$icapServer`:$icapPort$icapService ICAP/1.0`r`n"
$icapRequest += "Host: $icapServer`r`n"
$icapRequest += "User-Agent: PowerShell-ICAP-Client`r`n"
$icapRequest += "Encapsulated: req-hdr=0, req-body=" + ($fileSize + 4) + "`r`n`r`n"
# Define HTTP Encapsulation (Required by ICAP)
$httpRequest = "POST /test.html HTTP/1.1`r`n"
$httpRequest += "Host: example.com`r`n"
$httpRequest += "Content-Length: $fileSize`r`n"
$httpRequest += "Content-Type: application/octet-stream`r`n`r`n"
# Properly format file content as chunked encoding
$chunkedData = "$chunkSize`r`n"
$chunkedData += [System.Text.Encoding]::UTF8.GetString($fileContent) + "`r`n"
$chunkedData += "0`r`n`r`n" # End of chunk
# Combine ICAP and HTTP requests
$fullRequest = $icapRequest + $httpRequest + $chunkedData
# Create a TCP socket to communicate with the ICAP server
$tcpClient = New-Object System.Net.Sockets.TcpClient($icapServer, $icapPort)
$stream = $tcpClient.GetStream()
$writer = New-Object System.IO.StreamWriter($stream)
$reader = New-Object System.IO.StreamReader($stream)
# Send the properly formatted ICAP request
$writer.Write($fullRequest)
$writer.Flush()
# Receive and display ICAP response
$response = $reader.ReadToEnd()
Write-Output "ICAP Server Response:`n$response"
# Close the connection
$writer.Close()
$reader.Close()
$stream.Close()
$tcpClient.Close()
#### [Execute the script following the command](/docs/mdicap/v5.15.0/knowledge-base/how-to-send-a-file-to-icap-server-for-testing-the-functionalites#execute-the-script-following-the-command)

TEXTCopy.\icap_win.ps1 -icapServer <ICAP Server IP> -icapPort <ICAP Port> -filePath <Path to test file>

Example:

TEXTCopy.\icap_win.ps1 -icapServer "127.0.0.1" -icapPort 1344 -filePath "D:\eicar.txt"Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

<!-- source: https://www.opswat.com/docs/fenddiode/appendices/appendix-ii-list-of-supported-ftp-commands -->

# Appendix II: List of Supported FTP Commands

View as Markdown Ask ChatGPT about this page Ask Claude about this page

| Command | Definition |
| --- | --- |
| **ABOR** | Abort an active file transfer |
| **CWD*** | Change working director |
| **DELE** | Delete file |
| **EPRT** | Specifies an extended address and port to which the server should connect |
| **EPSV** | Enter extended passive mode |
| **FEAT** | Get the extended feature list implemented by the server. |
| **MODE** | Sets the transfer mode (Stream, Block, or Compressed) |
| **PASS** | Authentication password |
| **PASV** | Enter passive mode |
| **PORT** | Specifies an address and port to which the server should connect |
| **PWD** | Print working directory. Returns the current directory of the host. |
| **QUIT** | Disconnect |
| **REIN** | Re initializes the connection |
| **RNFR** | Rename file from |
| **RNTO** | Rename file to |
| **STOR** | Accept the data and to store the data as a file at the server site |
| **SYST** | System type |
| **TYPE** | Sets the transfer mode (Binary/ASCII) |
| **USER** | Authentication username |
| **XPWD** | Print the current working directory (code for firewalls that require four characters) |

*Note: When changing directories on the diode you must use absolute (full) paths. Using relative pathing will result in the output side being unable to upload the file.

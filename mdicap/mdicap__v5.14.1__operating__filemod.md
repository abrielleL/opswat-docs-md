<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/operating/filemod -->

# FILEMOD

Besides the standard REQMOD and RESPMOD, ICAP Server supports the FILEMOD (file modification) ICAP methods.

FILEMOD lets the client to pass a file name and path to the ICAP Server so that it can scan the file in place (rather than streaming the file to the ICAP Server through TCP for scanning).

The FILEMOD method deviates from the ICAP 1.0 specification that is defined in [RFC 3507](https://tools.ietf.org/html/rfc3507).

MetaDefender ICAP Server can be integrated to ICAP clients that implement the FILEMOD method. However, as FILEMOD is a non-standard implementation itself, the integration may require extra effort to work as desired.

**NOTE**: When FILEMOD is being used, and if your workflow rules are configured to **block** certain files due to file type mismatch, password-protected documents, scan errors or timeouts, etc, ICAP Server will directly delete those files when detected. To avoid incidental deletion of those blocked files, enable the settings “Quarantine blocked files” and “Override scan results classified as Allowed” within MetaDefender Core and select the desired result types to quarantine.

## [Example](/docs/mdicap/v5.14.1/operating/filemod#example)

## [Client FILEMOD request](/docs/mdicap/v5.14.1/operating/filemod#client-filemod-request)

FILEMOD icap://172.16.201.195:1344/ ICAP/1.0
Host: 172.16.201.195:1344
X-Filepath: C:\Viruses\eicar.com
Connection: close
Encapsulated: null-body=0
## [Server response to FILEMOD](/docs/mdicap/v5.14.1/operating/filemod#server-response-to-filemod)

This response returns a *403 Forbidden* status, which indicates that -in this example- a virus was found, which is indicated in the *X-Violations-Found* header.

ICAP/1.0 403 Forbidden.
ISTag: "1605188845"
Date: Thu Nov 12 13:47:25 2020 GMT
Service: MetaDefender ICAP Server
Service-ID: Metascan
X-Violations-Found: 1
eicar.com
EICAR Test String
11101
2
X-Outer-Container-Is-Mime: 0
Encapsulated: null-body=0

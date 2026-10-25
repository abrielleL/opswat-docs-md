<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-an-icap-request-looks-like- -->

# How an ICAP Request looks like?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

ICAP requests (defined in [**RFC 3507**](https://datatracker.ietf.org/doc/html/rfc3507)) are HTTP-like messages used to send content to the ICAP Server for processing.

**Basic format:**

<ICAP Method> <ICAP URI> ICAP/1.0
ICAP-Headers
Encapsulated-HTTP-Message

**EXAMPLE: REQMOD Request:**

REQMOD icap://icap.example.net/reqmod ICAP/1.0
Host: icap.example.net
Encapsulated: req-hdr=0, null-body=0
GET / HTTP/1.1
Host: example.com
## [**Key Elements:**](/docs/mdicap/v5.15.0/knowledge-base/how-an-icap-request-looks-like-#key-elements)

- **Request line:**

  - Defines the method and service:
  - `REQMOD` - modify HTTP request
  - `RESPMOD` - modify HTTP response
  - `OPTIONS` - query capabilities
  - `FILEMOD` - Transfer file data to ICAP server for processing
- **ICAP Headers**

  - Provide metadata (e.g., `Host`, `User-Agent`, `Preview`)
- **Encapsulated header (required)**

  - Specifies which HTTP parts are included and their offsets
  - *Example:*

Encapsulated: req-hdr=0, req-body=137

- **Embedded HTTP message**

  - The actual HTTP request or response being processed

Invalid ICAP requests — such as those with malformed structure, unsupported methods, or missing mandatory headers — are rejected by the ICAP server and result in a **400 (Bad Request)** **response**. Ensuring that requests follow the correct format, including a valid request line and properly defined Encapsulated header, is essential for successful processing.

## [**OPTIONS**](/docs/mdicap/v5.15.0/knowledge-base/how-an-icap-request-looks-like-#options)

Sent by the client to discover what methods and capabilities the ICAP server supports.

**Example request:**

OPTIONS icap://<ICAP-SERVER-HOST>:<ICAP-SERVER-PORT>/OMSScanResp-AV ICAP/1.0
Host: <ICAP-CLIENT-IP>:<ICAP-SERVER-PORT>
Allow: 206

**Example response:**

ICAP/1.0 200 OK
Methods: REQMOD, RESPMOD, FILEMOD
Service: MetaDefender ICAP Server
ISTag: "<ISTAG-VALUE>"
Max-Connections: 100
Options-TTL: 3600
Allow: 204
Preview: 1024
Transfer-Preview: *
Encapsulated: null-body=0
## [**REQMOD**](/docs/mdicap/v5.15.0/knowledge-base/how-an-icap-request-looks-like-#reqmod)

Used to intercept and scan or modify an outgoing HTTP request, such as a file upload.

**Example request:**

REQMOD icap://<ICAP-SERVER-HOST>:<ICAP-SERVER-PORT>/virus_scan ICAP/1.0
Host: <ICAP-SERVER-HOST>:<ICAP-SERVER-PORT>
Encapsulated: req-hdr=0, null-body=170
GET / HTTP/1.1
Host: <ORIGIN-SERVER-HOST>
Accept: text/html, text/plain
Accept-Encoding: compress
Cookie: <SESSION-COOKIE>
If-None-Match: "<ETAG-VALUE>"

**Example response:**

ICAP/1.0 200 OK
ISTag: "<ISTAG-VALUE>"
Date: Tue, 16 Feb 2016 11:51:03 GMT
Service: MetaDefender ICAP Server
X-Violations-Found: 0
Encapsulated: req-hdr=0, null-body=0
GET / HTTP/1.1
Host: <ORIGIN-SERVER-HOST>
Accept: text/html, text/plain
Accept-Encoding: compress
## [**RESPMOD**](/docs/mdicap/v5.15.0/knowledge-base/how-an-icap-request-looks-like-#respmod)

Used to intercept and scan or modify an HTTP response being returned to the client, such as a file download.

**Example request:**

RESPMOD icap://<ICAP-SERVER-HOST>:<ICAP-SERVER-PORT>/virus_scan ICAP/1.0
Host: <ICAP-SERVER-HOST>:<ICAP-SERVER-PORT>
Date: Tue, 16 Feb 2016 11:51:03 GMT
Encapsulated: req-hdr=0, res-hdr=618, res-body=831
X-Client-IP: <CLIENT-IP>
GET /eicar.dirty HTTP/1.1
Host: <ORIGIN-SERVER-HOST>
User-Agent: Mozilla/5.0
Accept-Encoding: gzip, deflate, sdch
HTTP/1.1 200 OK
Content-Disposition: attachment; filename="eicar.dirty"
Content-Length: 68
Content-Type: application/octet-stream
X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*

**Example response (threat detected):**

ICAP/1.0 403 Forbidden
ISTag: "<ISTAG-VALUE>"
Date: Tue, 16 Feb 2016 11:51:04 GMT
Service: MetaDefender ICAP Server
X-Violations-Found: 1
eicar.dirty
EICAR Test String
11101
2
Encapsulated: null-body=0
## [**FILEMOD**](/docs/mdicap/v5.15.0/knowledge-base/how-an-icap-request-looks-like-#filemod)

A non-standard extension that passes a local file path to the ICAP server for in-place scanning, without streaming the file over the network.

**Example request:**

FILEMOD icap://<ICAP-SERVER-HOST>:<ICAP-SERVER-PORT>/ ICAP/1.0
Host: <ICAP-SERVER-HOST>:<ICAP-SERVER-PORT>
X-Filepath: <PATH-TO-FILE>
Connection: close
Encapsulated: null-body=0

**Example response (threat detected):**

ICAP/1.0 403 Forbidden.
ISTag: "<ISTAG-VALUE>"
Date: Thu Nov 12 13:47:25 2020 GMT
Service: MetaDefender ICAP Server
Service-ID: Metascan
X-Violations-Found: 1
<FILENAME>
<THREAT-NAME>
<THREAT-ID>
<SEVERITY>
Encapsulated: null-body=0

**Example response (clean file):**

ICAP/1.0 204 No modifications needed
ISTag: "<ISTAG-VALUE>"
Date: Thu Nov 12 13:47:25 2020 GMT
Service: MetaDefender ICAP Server
Service-ID: Metascan
Encapsulated: null-body=0

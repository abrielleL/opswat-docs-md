<!-- source: https://www.opswat.com/docs/mdicap/operating/icap-server-response-codes -->

# ICAP Server response codes

MetaDefender ICAP Server supports following ICAP methods:

- REQMOD
- RESPMOD
- OPTIONS
- FILEMOD

Following is the list of available status codes associated to those ICAP methods that could be returned by MetaDefender ICAP Server:

| Status code | Description | ICAP method |
| --- | --- | --- |
| **100 Continue** | Signal client to continue sending data to ICAP Server after ICAP Preview message | REQMOD, RESPMOD |
| **200 OK** | The request has been processed successfully | REQMOD, RESPMOD, OPTIONS, FILEMOD |
| **204 No modification needed** | The request is clean and no modification is needed | REQMOD, RESPMOD |
| **400 Bad request** | Due to either invalid method of ICAP, or invalid header request, or missing mandatory header(s) | REQMOD, RESPMOD, OPTIONS, FILEMOD |
| **404 Not found** | ICAP Service is not found | REQMOD, RESPMOD, OPTIONS, FILEMOD |
| **403 Forbidden** | The request is infected and cannot be repaired | FILEMOD |
| **502 File unavailable** | Failed to open file | FILEMOD |

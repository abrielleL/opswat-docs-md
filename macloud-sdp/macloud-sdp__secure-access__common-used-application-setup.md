<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/common-used-application-setup -->

# Commonly Used Application Setup

Typical port and protocols for integrating applications with Software Defined Perimeter(SDP):

| **Application** | **Resources** | **Protocol** | **Description** |
| --- | --- | --- | --- |
| Cisco Umbrella | Make sure your Private Gateways DNS settings are pointing to the 2 Cisco Umbrella Virtual Appliance servers. |  |  |
| Exchange, On-premise | [https://mail.[COMPANY_NAME].com/owa/](https://mail.%5BCOMPANY_NAME%5D.com/owa/) |  |  |
|  | 443 | Both |  |
|  | 80 | Both |  |
|  | 4125 | Both |  |
|  | 3389 | Both |  |
|  | 389 | Both |  |
|  | 379 | Both |  |
|  | 390 | Both |  |
|  | 3268 | Both |  |
|  | 636 | Both |  |
|  | 3269 | Both |  |
|  | 143 | Both |  |
|  | 993 | Both |  |
|  | 110 | Both |  |
|  | 995 | Both |  |
|  | 119 | Both |  |
|  | 563 | Both |  |
|  | 80 | Both |  |
|  | 443 | Both |  |
|  | 25 | Both |  |
|  | 465 | Both |  |
|  | 691 | Both |  |
|  | 102 | Both |  |
|  | 135 | Both |  |
|  | 522 | Both |  |
|  | 53 | Both |  |
| Fiserv Nautilus | <https://nautilus.ins05.fiserv.com:5700/AppServer/service.asmx> | Both | Documentation and collaboration software |
|  | 5700 |  | The port the web server is running on. In this case is 5700 |
| Fiserv DNA | <https://dna01.opensolutionsasp.com:30350/saf> |  |  |
|  | 30350 |  | The port the web server is running on. In this case is 30350 |
| Ninja RMM | [https://rmm.[COMPANY_NAME].com](https://rmm.%5BCOMPANY_NAME%5D.com) |  |  |
|  | 443 | Both |  |
|  | 80 | Both |  |
|  | 10000 | Both |  |
| PDQ Patch Management | 8080 | UDP |  |
|  | 138 | UDP |  |
|  | 445 | Both |  |
|  | 139 | Both |  |
|  | 6336 | TCP |  |
|  | 7337 | TCP |  |
| RSA Portal | 443 | Both |  |
|  | 53 | Both |  |
|  | 445 | Both |  |
|  | 88 | Both |  |
|  | 135-139 | Both |  |
|  | 7004 | Both |  |
| RDP (Alternative port) | 8080 | Both |  |
| RDP (Standard) | 3389 | Both |  |
| Skype | 8080 | TCP |  |
|  | 3478-3481 | UDP |  |
|  | 50000-60000 | UDP |  |
|  | 1000-10000 | TCP |  |
|  | 16000-26000 | TCP |  |
| Windows Domain Controller/FileShare | [SERVER_NAME].[COMPANY_NAME].local |  |  |
|  | 8080 | Both |  |
|  | 445 | Both |  |
|  | 53 | Both |  |
|  | 67-68 | Both |  |
|  | 88 | Both |  |
|  | 389 | Both |  |
|  | 464 | Both |  |
|  | 135-139 | Both | May not be necessary for file share |

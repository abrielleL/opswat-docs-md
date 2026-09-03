<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/knowledge-base/how-to-simulate-icap-traffic-to-test-icap-functionality-using-te -->

# How to Simulate ICAP Traffic to Test ICAP Functionality Using Telnet?

## [**Telnet Installation**](/docs/mdicap/v5.14.1/knowledge-base/how-to-simulate-icap-traffic-to-test-icap-functionality-using-te#telnet-installation)

### [**Windows:**](/docs/mdicap/v5.14.1/knowledge-base/how-to-simulate-icap-traffic-to-test-icap-functionality-using-te#windows)

Make sure Telnet is enabled under "Turn Windows features on or off."

### [**Linux:**](/docs/mdicap/v5.14.1/knowledge-base/how-to-simulate-icap-traffic-to-test-icap-functionality-using-te#linux)

Make sure Telnet is installed on your system.

#### [Debian/Ubuntu-based distributions:](/docs/mdicap/v5.14.1/knowledge-base/how-to-simulate-icap-traffic-to-test-icap-functionality-using-te#debianubuntu-based-distributions)

BashCopysudo apt install telnet -y
#### [RHEL/CentOS/Fedora:](/docs/mdicap/v5.14.1/knowledge-base/how-to-simulate-icap-traffic-to-test-icap-functionality-using-te#rhelcentosfedora)

BashCopysudo yum install telnet -y
#### [For newer versions (CentOS 8+, RHEL 8+, Fedora):](/docs/mdicap/v5.14.1/knowledge-base/how-to-simulate-icap-traffic-to-test-icap-functionality-using-te#for-newer-versions-centos-8-rhel-8-fedora)

BashCopysudo dnf install telnet -y
#### [Verify Installation:](/docs/mdicap/v5.14.1/knowledge-base/how-to-simulate-icap-traffic-to-test-icap-functionality-using-te#verify-installation)

After installation, check if Telnet is installed by running:

BashCopytelnet --version
## [Simulate ICAP traffic using Telnet](/docs/mdicap/v5.14.1/knowledge-base/how-to-simulate-icap-traffic-to-test-icap-functionality-using-te#simulate-icap-traffic-using-telnet)

### [**1. Open a Telnet Connection**](/docs/mdicap/v5.14.1/knowledge-base/how-to-simulate-icap-traffic-to-test-icap-functionality-using-te#1-open-a-telnet-connection)

Use the following command in a terminal or command prompt:

BashCopytelnet <ICAP_SERVER> <ICAP_PORT>

Example:

BashCopytelnet 192.168.233.132 1344
### [**2. Construct an ICAP Request**](/docs/mdicap/v5.14.1/knowledge-base/how-to-simulate-icap-traffic-to-test-icap-functionality-using-te#2-construct-an-icap-request)

After connecting via telnet, Copy and paste the ICAP request. Below is an example request for REQMOD (Request Modification):

ICAP REQMOD Request Example:

BashCopyREQMOD icap://192.168.233.132/OMSScanReq-AV ICAP/1.0
Host: 192.168.1.100
Encapsulated: req-hdr=0, null-body=120
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Telnet-ICAP

After typing, **press Enter twice** to send the request.

If the request is successful, you will see the response as the output.

On the **MetaDefender ICAP Console Management**

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).

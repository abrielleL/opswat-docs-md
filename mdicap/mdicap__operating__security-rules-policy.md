<!-- source: https://www.opswat.com/docs/mdicap/operating/security-rules-policy -->

# Workflow Management

MetaDefender ICAP Server's workflows can be configured under **Workflow** **Management**

## [Workflow Management overview](/docs/mdicap/operating/security-rules-policy#workflow-management-overview)

Workflow help to assign security policies to specific requests.

A Workflow consists of two parts:

- Request filter
- Security policy definition

## [Request filter](/docs/mdicap/operating/security-rules-policy#request-filter)

Based on header values or source address, request filters select requests on which the assigned security policy will be applied. Request filters can be set up on the **Request filters** tab while creating or editing a security rule.

Filtering can be based on source address, ICAP, HTTP or custom headers. The following parameters must be provided to create a filter condition:

- Header name: name of the header to look up.
- ICAP client address: address of the ICAP client
- Match type: the value of the referred header must be equal to, contain, start with, or end with the provided value.
- Value: the value to match.

Note

If a header with the referred header name does not exist in the request, then this condition won't match.

### [Filter parts](/docs/mdicap/operating/security-rules-policy#filter-parts)

A filter may consist of four parts:

1. Host IP/Domain conditions
2. Client IP conditions
3. ICAP client address
4. Generic conditions

Note

There is **AND** relation among the above parts of the filter.

#### [Host IP/Domain conditions](/docs/mdicap/operating/security-rules-policy#host-ipdomain-conditions)

| Header name | Match type |
| --- | --- |
| Host | Wildcard matching (glob) |

The Host header usually contains the requested URI.

Note

There is **OR** relation among entries in Host IP/Domain conditions.

#### [Client IP conditions](/docs/mdicap/operating/security-rules-policy#client-ip-conditions)

| Header name | Match type |
| --- | --- |
| X-Client-IP | Wildcard matching (glob) |

The X-Client-IP header usually contains the IP of the machine from which the request was originally sent.

Note

There is **OR** relation among the Client IP conditions.

#### [Wildcard matching examples](/docs/mdicap/operating/security-rules-policy#wildcard-matching-examples)

| Example pattern | Matches | Does not match |
| --- | --- | --- |
| 127.0.0.* | 127.0.0.1, 127.0.0.150 | 127.0.100.1, 127.5.0.1 |
| [www.example.co](http://www.example.co)? | [www.example.com](http://www.example.com) | [www.example.co](http://www.example.co) |
| [ab]cd | acd, bcd | cd, ecd |
| abc | abc | cba, xyz |

Warning

Please note the difference between the *Client IP* conditions and the *ICAP client IP* conditions: the client IP is the node from whom the original request is sent, while the ICAP client is the network element that is in direct connection with the ICAP Server (e.g. proxy).

#### [ICAP client IP conditions](/docs/mdicap/operating/security-rules-policy#icap-client-ip-conditions)

The ICAP client address is the address from where the ICAP request is originated (for example a proxy server).

Success

The match type is wildcard matching (glob).

Note

There is **OR** relation among the ICAP client address conditions.

Warning

Please note the difference between the *Client IP* conditions and the *ICAP client IP* conditions: the client IP is the node from whom the original request is sent, while the ICAP client is the network element that is in direct connection with the ICAP Server (e.g. proxy).

#### [Generic conditions](/docs/mdicap/operating/security-rules-policy#generic-conditions)

Using generic conditions, filters can be set up to any headers.

Info

As an example *Host IP/Domain* and *Client IP* conditions could also be set up as generic conditions.

Note

There is **AND** relation among the generic conditions.

### [Header references](/docs/mdicap/operating/security-rules-policy#header-references)

Filtering can be based on ICAP, HTTP or even custom headers. For an incomplete reference of possible headers consult the following sources:

- HTTP

  - [IANA](https://www.iana.org/assignments/message-headers/message-headers.xml)
  - [Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
- ICAP: [IETF](https://tools.ietf.org/html/rfc3507)
- Custom: Initially, it was recommended to begin naming custom headers with X- , however, according to [RFC 6648](https://tools.ietf.org/html/rfc6648) , this recommendation has since been deprecated.

## [Workflow policy](/docs/mdicap/operating/security-rules-policy#workflow-policy)

A Workflow policy consists of the SCAN, DATA TRICKLING, ADVANCED and the SOAP/JSON (support since v5.3.0) settings.

### [Scan settings](/docs/mdicap/operating/security-rules-policy#scan-settings)

The scan policy can be set up on the **Scan** tab while creating or editing a security rule.

The following options are available:

1. ALLOW SCAN: enable or disable scanning of requests. Default is enabled.

   1. METADEFENDER CORE: MetaDefender Core type server profile to which requests are sent for scanning. Default is *None* .
   2. SCAN TIMEOUT: ICAP Server will try to get the scan results for the timeout defined here. If the timeout elaplses then the request gets blocked. Default is 0.

      1. Valid range: 0 .. 86400
      2. 0 (zero) means that there is no timeout: ICAP Server will wait for the results for any long time.

Note

When scanning is disabled, all requests will be accepted.

### [Data trickling](/docs/mdicap/operating/security-rules-policy#data-trickling)

Data trickling preferences can be set on the **Data trickling** tab while creating or editing a security rule. For further details about data trickling see [4.7 Data trickling](/docs/mdicap/operating/data-trickling).

The following options are available:

1. ENABLE DATA TRICKLING: enable releasing drips of the original contents even before the scanning completes.

Warning

Risk of potential threats allowed

WARNING!

Given by the nature of the thing, enabling data trickling may cause the ICAP Server to release potentially malicious content.

Always enable data trickling with care; only if you know what you are doing, if you are aware of the risk, and if you accept this risk.

1. FIRST DRIP: settings related to the first drip of the original content

1. DELAY: Delay of the first drip –after the contents have been submitted for scanning– in seconds.

2. SIZE: Size of the first drip –after the contents have been submitted for scanning– in kilobytes.

2. ADDITIONAL DRIPS

1. DELAY: Delay of each consecutive drips –after the first, or any other previous drip– in seconds.

2. SIZE: Size of each consecutive drips –after the first, or any other previous drip– in kilobytes.

3. ENABLE TO WITHHOLD: Whether to allow or not to withhold the last portion of the original contents from being dripped before the scanning completes.

Warning

Risk of releasing malicious object

If ENABLE TO WITHHOLD is not set, and the end of the file is reached any time during the trickling, then the whole original, potentially malicious content has been already released.

Always set ENABLE TO WITHHOLD, except only if you know what you are doing, if you are aware of the risk, and if you accept this risk.

1. Size: Size of withheld data in kilobytes.

### [Allow list](/docs/mdicap/operating/security-rules-policy#allow-list)

Support since ICAP v5.9.0, the FileType engine has already integrated to MD ICAP Server and supported set the Allow List for each workflow.

When the file type in Allow List is checked then the files with corresponding file type will not be send to MD Core backend for scanning

Warning

User who is using Rocky Linux 9.x/Red Hat 9.x must install libnsl manually

refer to Other software requirements

### [Block Page](/docs/mdicap/operating/security-rules-policy#block-page)

refer to [Replacing the default block page](/docs/mdicap/configuration/customizing-the-block-page#replacing-the-default-block-page)

### [Advanced settings](/docs/mdicap/operating/security-rules-policy#advanced-settings)

Some default security behaviors of the system can be modified on the **Advanced** tab while creating or editing a security rule.

The following options are available:

1. OVERRIDE SCAN RESULTS CLASSIFIED AS ALLOWED: enable or disable overriding the following default security behaviors all together.

   1. MULTIPART PARSING ERROR: Requests with multipart content are parsed for boundary and control header correctness. By default requests with mutlipart parsing error are rejected by MetaDefender ICAP Server. Enabling this option will accept such requests. (For further details about multipart content see [RFC 1341](https://tools.ietf.org/html/rfc1341) and [RFC 2388](https://tools.ietf.org/html/rfc2388).)
   2. CORE BUSY: By default MetaDefender ICAP Server rejects requests when none of the Cores of the applied server profile can accept the scan requests due to overload. Enabling this option scanning will be skipped and the request will be accepted when all Cores are busy.
   3. CORE RULE FILE SIZE LIMIT EXCEEDED: By default MetaDefender Core blocks a file that exceeds the file size limit configured for the Core rule (see [3.6.2. Workflow template configuration](https://onlinehelp.opswat.com/corev4/3.6.2._Workflow_template_configuration.html) and [3.6.4. Workflow rule configuration](https://onlinehelp.opswat.com/corev4/3.6.4._Workflow_rule_configuration.html) chapters in [MetaDefender Core v4 User Guide](https://onlinehelp.opswat.com/corev4)) applied for the ICAP Server security rule. Enabling this option results the oversized request to bypass scanning.
   4. SCAN TIMEOUT: By enabling this option MetaDefender ICAP Server will allow requests whose scan timed out.
   5. CORE SERVER ERROR: By enabling this option MetaDefender ICAP Server will allow requests which had a general MetaDefender Core error during their processing. This means every error where MetaDefender Core responded with the status code 500 and is not listed above as a specific case.
2. ACTION FOR NOT SUPPORTED ENCODINGS: MetaDefender ICAP Server supports *gzip*, *deflate*, *brotli, zstd* and *base64* encoding only. By default requests with any other encoding are rejected by default. Here you can select your preferred action for these kind of requests.

   1. BLOCK: Block the request. This is the default option.
   2. SCAN WITHOUT DECODING: Send the content without decoding towards MetaDefender Core for processing and continue serving the request based on the processing result.
   3. ALLOW: Allow the request without processing the content.
3. ACTION FOR DECODING ERRORS: MetaDefender ICAP Server supports *gzip*, *deflate*, *brotli, zstd* and *base64* encoding of request contents. By default requests with encoding error are rejected. Here you can select your preferred action for these kind of requests.

   1. BLOCK: Block the request. This is the default option.
   2. SCAN WITHOUT DECODING: Send the content without decoding towards MetaDefender Core for processing and continue serving the request based on the processing result.
   3. ALLOW: Allow the request without processing the content.
4. Override Processing history (refer to [Override the processing history](/docs/mdicap/configuration/override-the-processing-history))
5. Add header to Metadata (In MetaDefender Core): Support since ICAP v5.8.0, Allow to specific any header from ICAP header or HTTP header can be audited in MetaDefender Core backend server's corresponding JSON processing details in the metadata field (displayed in metadata column of Metadefender Core's Processing history)

### [Content encoded (SOAP/JSON/Form URLEncoded)](/docs/mdicap/operating/security-rules-policy#content-encoded-soapjsonform-urlencoded)

Enabling MetaDefender ICAP Server to parse SOAP / JSON formatted message, then extract and decode base64 data which is embedded in the message, before sending to MetaDefender Core for further threat analysis.

Info

This configuration has been supported since MetaDefender ICAP Server version 5.3.0

Notes

Node path to data, and encoded type in JSON/SOAP message must be specified. Make use to use "/" to separate the node path.

When SOAP or JSON option is enabled:

- The sub-setting "**Limit file size scan**" will be auto applied. This limit is for SOAP / JSON entire message.

  - Acceptable range is [1, 100] MB
  - By default, the limit is 10MB
  - When size of request exceeds the configured limit, then scan request will be blocked (reason: File size exceeded).
- "**Scan content**" option, when select "**Scan whole contents**" then MetaDefender ICAP Server will process entire content of SOAP / JSON message (including embedded Base64 encoded data, and the rest of SOAP / JSON message).

  - Expecting longer processing time for SOAP / JSON message when enabled.
- Parsing JSON message, especially when in large size, will occupy system main memory (RAM) much.

  - Available memory (RAM) must be equal or greater: ***Number scan request in parallels * Limit file size scan***
#### [Node path configuration for SOAP message](/docs/mdicap/operating/security-rules-policy#node-path-configuration-for-soap-message)

**Example:**

Configuring MetaDefender ICAP Server to process the Base64 encoded data which is embedded in SOAP message with node **api:FileBase64String**

XmlCopy<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
<soapenv:Header xmlns:api="http://www.crmnext.com/api/"/>
<soapenv:Body xmlns:api="http://www.crmnext.com/api/">
<api:scan>
<api:objects>
<api:Description>Test data</api:Description>
<api:FileBase64String><!--- Base64 encodded data here -->/</api:FileBase64String>
</api:objects>
</api:scan>
</soapenv:Body>
</soapenv:Envelope>

Then the node path to scan FileBase64String is:

node pathCopy/soapenv:Envelope/soapenv:Body/api:scan/api:objects/api:FileBase64String

How to specific path for list element (Array) in SOAP

Rule:

- Do not input the index to access 1st element
- From 2nd element, but input the access index (start with 2)

E.g:

*<level>*

*<node>data1</node>*

*<node>data2</node>*

*<node>data3</node>*

*<node>data4</node>*

*</level>*

- The path to get data1: */level/node*
- The path to get data2: */level/node[2]*
- The path to get data3: */level/node[3]*
- The path to get data4: */level/node[4]*

__

From MD ICAP v5.7.0, to scan all 4 nodes, We can set by 1 path only: **/level/node[*]**

#### [Node path configuration for JSON message](/docs/mdicap/operating/security-rules-policy#node-path-configuration-for-json-message)

**Example:**

Configuring MetaDefender ICAP Server to process the Base64 encoded data which is embedded in JSON message with node **api:FileBase64String**

JsonCopy{
"Envelope": {
"Body": {
"scan": {
"objects" : {
"Description": "Test data",
"FileBase64String": "Base64 encodded data here"
}
}
}
}
}

Then the node path to scan FileBase64String is:

node pathCopy/Envelope/Body/scan/objects/FileBase64String

How to specific path for list element (Array) in JSON

Rule: to access array element must input the index (index is started from 1)

e.g:

{

"level": [

{

"node": "node1"

},

{

"node": "node2"

},

{

"node": "node3"

},

]

}

- Path to access node 1: /level[1]/node
- Path to access node 2: /level[2]/node
- Path to access node 3: /level[3]/node

From MD ICAP v5.7.0, to scan all 3 nodes, We can set by 1 path only: **/level[*]/node**

#### [Node path configuration for Form URL Encoded](/docs/mdicap/operating/security-rules-policy#node-path-configuration-for-form-url-encoded)

Example: configure Metadefender ICAP server to process base64 encoded data which is embedded in Form URL Encoded with

BashCopyFileBase64String=base64data1&Filename=somefilename

Then the node path to scan with the file name specific

Warning

Rule:

- Do not input the index to access 1st element
- From 2nd element, but input the access index (start with 2)

E.g: node=dbase64data1&node=dbase64data2&node=dbase64data3&node=dbase64data4

- The path to get data1: **/node**
- The path to get data2: **/node[2]**
- The path to get data3: **/node[3]**
- The path to get data4: **/node[4]**

From MD ICAP v5.7.0, to scan all 4 nodes, We can set by 1 path only: **/node[*]**

### [Rule Order](/docs/mdicap/operating/security-rules-policy#rule-order)

Several security rules can be created that may target different requests from different hosts going to different URL. However, care must be taken how these rules are set up and ordered, as there is a first match and a no match policy.

Specific rules should come first while generic rules should go at last.

Order of evaluation of security rules for a match

### [First match policy](/docs/mdicap/operating/security-rules-policy#first-match-policy)

If there are more matching rules in the system, then the request will be accepted or rejected according to the security policy of the first matching rule in the list.

### [No match policy](/docs/mdicap/operating/security-rules-policy#no-match-policy)

If there is no matching rule in the system (or no rule at all), then the request will be rejected.

The goal of the [147167977](/docs/mdicap/operating/security-rules-policy#src-4864672) is to have a rule in the system that matches in the end.

Note

Deleting all security rules from the system results all requests being blocked.

## [Security Rule Management](/docs/mdicap/operating/security-rules-policy#security-rule-management)

The Security Rule Management screen lists the existing security rules in the system.

## [Default security rule](/docs/mdicap/operating/security-rules-policy#default-security-rule)

After installation a default security rule is created with the following parameters:

| Name | Request filters | Allow scan | Applied core rule | Advanced |
| --- | --- | --- | --- | --- |
| Default | *none* | Yes | Automatic | *none* |

Note

The Default security rule matches any request. It will enforce scanning with automatically selected Core rule. It does not override any default advanced setting.

## [Functions](/docs/mdicap/operating/security-rules-policy#functions)

Besides listing existing security rules the Security Rule Management screen provides the following functions:

- Add new security rule
- Clone an existing security rule
- Modify (and view) existing security rule's properties
- Delete existing security rules

## [Use case examples](/docs/mdicap/operating/security-rules-policy#use-case-examples)

## [Enable anti-malware test site for test clients](/docs/mdicap/operating/security-rules-policy#enable-anti-malware-test-site-for-test-clients)

The site [*www.eicar.org*](http://www.eicar.org) is created to test anti-malware solutions. Under the URI <http://www.eicar.org/download/eicar.com.txt> there is a malware test file that is forbidden by MetaDefender ICAP Server by default:

$ wget http://www.eicar.org/download/eicar.com.txt
--2017-04-18 17:06:02-- http://www.eicar.org/download/eicar.com.txt
Connecting to 127.0.0.1:3128... connected.
Proxy request sent, awaiting response... 403 Forbidden
2017-04-18 17:06:03 ERROR 403: Forbidden.

Create the following rule (in the actual test the client browser, the proxy and the MetaDefender ICAP Server is on the same machine, that is the reason for the *Client IP* setting *127.0.0.1*):

#### [Filters:](/docs/mdicap/operating/security-rules-policy#filters)

#### [Scan Settings:](/docs/mdicap/operating/security-rules-policy#scan-settings)

Place it before the *Default* rule. Now the request is served:

$ wget http://www.eicar.org/download/eicar.com.txt
--2017-04-18 17:15:56-- http://www.eicar.org/download/eicar.com.txt
Connecting to 127.0.0.1:3128... connected.
Proxy request sent, awaiting response... 200 OK
Length: 68 [application/octet-stream]
Saving to: ‘eicar.com.txt.3’
 
100%[======================================>] 68 --.-K/s in 0s
 
2017-04-18 17:15:56 (20.2 MB/s) - ‘eicar.com.txt.3’ saved [68/68]

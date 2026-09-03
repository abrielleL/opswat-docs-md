<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/knowledge-base/how-do-i-setup-base64-content-scanning-for-unknown-requests-and- -->

# How do I setup base64 content scanning for unknown requests and responses?

MetaDefender ICAP Server supports parsing SOAP/JSON/Form URL Encoded formatted messages, then extracts and decodes the embedded base64 data, before sending to MetaDefender Core for further analysis.

For more details on this feature, please refer to the workflow management documentation on [Content encoded (SOAP/JSON/Form URL Encode)](https://www.opswat.com/docs/mdicap/operating/security-rules-policy#content-encoded-soapjsonform-urlencoded).

Info:

SOAP/JSON has been supported since MetaDefender ICAP Server version 5.3.0.

Form URL Encoded support has been supported since MetaDefender ICAP Server version 5.7.0.

That said, there are certain cases where the node containing the base64 encoded message isn’t known yet. You can determine this by simply **viewing the network traffic and inspecting the requests/responses**.

For example, when uploading a PBIX file to Power BI, that file is encoded as base64 in a JSON formatted message. When no configuration has been added for this, the content shows up on MetaDefender Core as JSON, without decoding the base64 content and analyzing the file:

To determine which specific node contains the base64 encoded file, you can open your **browser’s developer mode** (default key is F12 for most browsers) before uploading to Power BI, and inspect the request/response’s payload in the “Network” tab:

Developer mode view

1. Click the request that was generated when you upload the file to Power BI.
2. This gives the following JSON payload:

Alternatively, you can use a packet capture software such as Wireshark to capture the request and examine its body:

- **Note**: Wireshark is provided by 3rd party developers and is not developed or maintained by OPSWAT.

Wireshark packet capture

Now that the specific node containing the base64 encoded file is known, go to MetaDefender ICAP Server’s workflow configuration and add the following:

- Content Encoded → JSON:

  - Node selector
  - (Optional) File name

Once this is added, MetaDefender ICAP Server will be able to parse the JSON body of the request and decode the base64 encoded data, before sending to MetaDefender Core as a file named “data.pbix”.

Using the same example above, if the base64-encoded file is embedded in SOAP message, upon inspecting the payload of the request, you may see the following XML format:

Then configure in MetaDefender ICAP’s workflow with the following:

- Content Encoded → SOAP:

Similarly, if the base64-encoded file is embedded in Form URL Encoded, upon inspecting the payload of the request, you may see the following:

Then configure in MetaDefender ICAP’s workflow with the following:

- Content Encoded → Form URL Encoded:

Support:

For further assistance regarding **Setting up base64 content scanning for unknown request/response**, please follow these instructions [**creating a support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

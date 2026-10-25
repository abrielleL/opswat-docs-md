<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/operating/icap-response-headers -->

# ICAP response headers

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Besides the standard ICAP headers following response headers are used by the MetaDefender ICAP Server:

| Header name | Description | Example | Note |
| --- | --- | --- | --- |
| X-Blocked-Reason | MetaDefender specific custom header. Contains the blocking reason of the content. | X-Blocked-Reason: Infected | It is available only if the content was scanned and some violations were found. |
| X-ICAP-Profile | Contains the applied workflow's name. | X-ICAP-Profile: Proxy | It is available only if the file was scanned. |
| X-Response-Info | Contains the one word description of the action the ICAP server applied on the request. | X-Response-Info: Allowed X-Response-Info: Blocked X-Response-Info: Options | This header is available in all responses sent by the ICAP server. |
| X-Response-Desc | Contains the blocking reason. | X-Response-Desc: Infected X-Response-Desc: Encrypted Archive | The header is available in all "blocked" responses. In case of the content was scanned and some violations were found, the returned string is equivalent to X-Blocked-Reason's value. |
| X-Virus-ID | Contains a short description of the threat that was found in the content. If multiple threats were found, only the first one is returned. | X-Virus-ID: EICAR Test String X-Virus-ID: Encrypted Archive | The header is available only if the content was scanned and some violations were found. |
| X-Infection-Found | Contains the description of the threat that was found in the content. If multiple threats were found, only the first one is returned. The value is a semicolon separated list with three parameters:   - Type    - 0: Infection has been found   - 2: Container violation has been found - Resolution:    - 0: The suspicious content was not repaired - Threat: Threat name | X-Infection-Found: Type=0; Resolution=0; Threat=EICAR Test String; X-Infection-Found: Type=2; Resolution=0; Threat=Encrypted Archive; | The header is present only if the content was scanned and some violations were found. |
| X-Violations-Found | Contains the detailed description of the violations that were found. If the scanned content was an archive, the scan results for the contained files too are listed. If multiple threats were found for a single file, only the first one is returned. The structure of the header value is the following: The first line contains the number of the reported violations. The following lines contain the details. Filename Threat name ProblemID (currently 0 returned for all threats) ResolutionID:   - 0: File was not repaired - 1: File was repaired - 2: Violating part was removed | X-Violations-Found: 2 test.zip EICAR Test String 00 \eicar.txt EICAR Test String 00 | The header is present only if the content was scanned and some violations were found. |
| X-Include | Contains the list of requested headers, that the ICAP clients should add to the requests, if the information is available. | X-Include: X-Client-IP | The header is present only in Options responses. |

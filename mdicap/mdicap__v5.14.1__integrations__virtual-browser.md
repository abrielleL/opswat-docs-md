<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/virtual-browser -->

# Virtual Browser

Virtual Browser only supports AV multi-scanning. It does not accept modified files in the response (e.g. from CDR or DLP).

**Important**: The default scan timeout for Virtual Browser is 60 seconds. If this timeout needs to be adjusted to handle large and complex files, please contact Virtual Browser support

Note: This document was made base on Virtual Browser v4.0.6

## [Integration With MD ICAP Server](/docs/mdicap/v5.14.1/integrations/virtual-browser#integration-with-md-icap-server)

Configuration → General Setup → ICAP-RESPMOD

Input the address into ICAP URL with schema: ICAP://Address/OMSScanReq-AV

E.g: ICAP://10.40.168.135:1344/OMSScanReq-AV

Hit test button to make sure the integration is working

## [Enable File Scan](/docs/mdicap/v5.14.1/integrations/virtual-browser#enable-file-scan)

The file scan must be enabled by Files Rules (Configuration → Files rules)

check “Enabled” for File Analysis of each Files rules

## [Verification](/docs/mdicap/v5.14.1/integrations/virtual-browser#verification)

Download the eicar zip file over Virtual Browser:

e.g: https://virtualserverhost/vb/?https://www.eicar.org/download/eicar_com-zip/

<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/cross-domain-api -->

# Cross-domain API

Although cookie and client certificate integration methods work well under most scenarios. However, both methods heavily depend on browser applications and sometimes require end-users interaction which could introduce usability issues. My OPSWAT Central Management now offers a cross-domain API for you to integrate with your solution. This method leverages JSONP technology to overcome the cross-domain restrictions imposed by browsers' same-origin policy that limits access to resources retrieved from origins other than the one the page was served by.

The cross-domain API can be enabled on My OPSWAT Central Management console as the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/dyhyz6v76hv7pcherbumh4hz0cmwgpy4xks0qcjavzjt0466yz3c8dhv3os19hco.png)

Once the cross-domain API setting is enabled, MetaDefender Endpoint tries to open a cross-domain API at the configured port on an endpoint. Please make sure that the configured port is valid and not used by any existing applications running on the same endpoint.

Whenever  MetaDefender Endpoint is uninstalled/stopped, the cross-domain API will be closed and the configured port will be released on the endpoint.

## API Description

**Request**

|  | Description |
| ---- | ---- |
| **URL path** | [https://eapi.opswatgears.com:[configured](https://eapi.opswatgears.com:%5C%5Bconfigured)`port]/opswat/devinfo` |
| **URL path (API V3)** | [https://eapi.opswatgears.com:[configured](https://eapi.opswatgears.com:%5C%5Bconfigured/)`port]/opswat/3/devinfo` |
| **Method** | GET |

In which:

- configured port: the port you configured for the cross-domain API settings on My OPSWAT Central Management account which the endpoint is reporting to.
- eapi.opswatgears.com is resolved as 127.0.0.1. If endpoints are running proxy, you need to add exception on the proxy settings to ignore queries to [eapi.opswatgears.com](http://eapi.opswatgears.com).

For example:

```plaintext
https://eapi.opswatgears.com:11369/opswat/devinfo
API V3: https://eapi.opswatgears.com:11369/opswat/3/devinfo
```

**Success response**

The response json will be padded by the value of "callback" parameter

```plaintext
{
	"code": number,
	"description": string,
	"info": {
		"hwid": string
	}
}
```

**Error response**

```plaintext
{
	"code": number,
	"description": string
}
```

| Key | DataType | Definition |
| ---- | ---- | ---- |
| code | number | Status code. Values could be: - 0: success - -30: Timeout - -31: API not found - -32: Verification failed - -41: Failed to get hardware id |
| description | string | result details |
| info | object | device information |
| info.hwid | string | device id of the device. This information is used to query device information from the cloud. |

## Sample code V1 (Don't use JWT token to verify the response data - Less secure)

**Client sample** (you can download from [here](https://onlinehelp.opswat.com/metaaccess/attachments_5719785_1_client_sample_code.rar))

```plaintext
<html>
    <head>
    </head>
    <body>
		<div style="margin-top: 25px; margin-bottom: 25px"> THIS IS A DEMO TO RETRIVE DEVICE ID OF THE LOCAL DEVICE</div>
        <div id="loader" style="display: none; position: fixed;left: 0px;top: 0px;width: 100%;height: 100%;z-index: 9999;background: url('page-loader.gif') 50% 50% no-repeat rgb(249,249,249);"></div>
        Server Port: <input type="text" id="server_port" value="11369" placeholder="11369"/><p>
 
        <div>
            <input type="button" value="Get Agent Info" onClick="submitGetAgentInfo()">
            <div id="error_msg" style="color:  red; margin-top: 10px;"> </div>
        </div>
 
        <div id="hwid_field"> </div>
        <script  type="text/javascript" src="jquery-3.1.1.min.js"></script>
        <script  type="text/javascript" src="opswat.jsonp.js"></script>
        <script type="text/javascript">
            function myCallback( data_back ){
                $('#loader').hide();
                // callback function to handle response from cloud
                if ( data_back.code < 0 ) {
                    $('#error_msg').html("Error: " + data_back.description );
                    return;
                }

                $('#hwid_field').text('Device ID: '+  data_back.info.hwid);
            }
            function submitGetAgentInfo()
            {
                $('#hwid_field').text('');
                $('#error_msg').html('');
                $('#loader').show();
                // Using Opswat lib prototype to make a request to cloud
                var server_port = $('#server_port').val();
                var casb = new OpswatJSONP();
                casb.jsonp({
                    'serverPort': server_port,
                    'callback' : myCallback
                });
            }
    </script>
    </body>
</html>
```

Note: you can find **jquery-3.1.1.min.js** and **opswat.jsonp.js** in the [sample package](https://onlinehelp.opswat.com/metaaccess/attachments_5719785_1_client_sample_code.rar).

## Sample code V2: (Using JWT token to verify the response data - more secure)

**Client sample** (you can download from [client_sample_code_v2.zip](https://onlinehelp.opswat.com/metaaccess/attachments_5719783_1_client_sample_code_v2.zip))

```plaintext
<html>
    <head>
    </head>
    <body>
        <div id="loader" style="display: none; position: fixed;left: 0px;top: 0px;width: 100%;height: 100%;z-index: 9999;background: url('page-loader.gif') 50% 50% no-repeat rgb(249,249,249);"></div>
        Server Port: <input type="text" id="server_port" value="11369" placeholder="11369"/><p>
 
        <div>
            <input type="button" value="Get Agent Info - JWT (More Secure)" onClick="submitGetAgentInfoJWT()">
            <div id="error_msg" style="color:  red; margin-top: 10px;"> </div>
        </div>
 
        <div id="hwid_field"> </div>
        <script  type="text/javascript" src="jquery-3.1.1.min.js"></script>    <!-- required, go along with opswat.casb.js -->
        <script  type="text/javascript" src="jsrsasign-all-min.js"></script>    <!-- required, go along with opswat.casb.js -->
        <script  type="text/javascript" src="opswat.casb.js"></script>    <!-- Opswat library -->
        <script type="text/javascript">
            function myCallback( data_back ){
                $('#loader').hide();
                // callback function to handle response from cloud
                if ( data_back.code < 0 ) {
                    $('#error_msg').html("Error: " + data_back.description );
                    return;
                }

                $('#hwid_field').text('Hardward ID: '+  data_back.info.hwid);
            }
            function submitGetAgentInfoJWT()
            {
                $('#hwid_field').text('');
                $('#error_msg').html('');
                $('#loader').show();
 
                //We need to generate a session id for every request to recive the dynamic response and verify it when we receive the response from Jsonp server
                var sessionId = uuidv4();
 
                // Using Opswat lib prototype to make a request to cloud
                var server_port = $('#server_port').val();
                var casb = new OpswatCASB();
                casb.jsonp({
                    'serverPort': server_port,
                    'callback' : myCallback,
                    'sessionId' : sessionId
                });
            }
 
            function uuidv4() {
              return ([1e7]+-1e3+-4e3+-8e3+-1e11).replace(/[018]/g, c =>
                (c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> c / 4).toString(16)
              );
            }
    </script>
    </body>
</html>
```

Note: you can find **jquery-3.1.1.min.js**, jsrsasign-all-min.js  and **opswat.jsonp.js** in the [client_sample_code_v2.zip](https://onlinehelp.opswat.com/metaaccess/attachments_5719783_1_client_sample_code_v2.zip).

## Sample code V3: (Using JWT token to verify the response data and support Cross-Origin Resource Sharing - CORS)

**Client sample** (you can download from [*client_sample_code_v3.zip*](https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/client_sample_code_v3.zip))

```html
<html>
    <head>
    </head>
    <body>
        <div id="loader" style="display: none; position: fixed;left: 0px;top: 0px;width: 100%;height: 100%;z-index: 9999;background: url('page-loader.gif') 50% 50% no-repeat rgb(249,249,249);"></div>
        Server Port: <input type="text" id="server_port" value="11369" placeholder="11369"/><p>

        <div>
            <input type="button" value="Get Agent Info - JWT (More Secure) V3" onClick="submitGetAgentInfoJWT(true)">
            <div id="error_msg" style="color:  red; margin-top: 10px;"> </div>
        </div>

        <div id="hwid_field"> </div>
        <script  type="text/javascript" src="jquery-3.1.1.min.js"></script>    <!-- required, go along with opswat.casb.js -->
        <script  type="text/javascript" src="jsrsasign-all-min.js"></script>    <!-- required, go along with opswat.casb.js -->
        <script  type="text/javascript" src="opswat.casb.js"></script>    <!-- Opswat library -->
        <script type="text/javascript">
            function myCallback( data_back ){
                $('#loader').hide();
                // callback function to handle response from cloud
                if ( data_back.code < 0 ) {
                    $('#error_msg').html("Error: " + data_back.description );
                    return;
                }

                $('#hwid_field').text('Hardward ID: '+  data_back.info.hwid);
            }
            function submitGetAgentInfoJWT(isV3 = false)
            {
                // console.log(isV3);
                $('#hwid_field').text('');
                $('#error_msg').html('');
                $('#loader').show();
                var sessionId = uuidv4();
                // Using Opswat lib prototype to make a request to cloud
                var server_port = $('#server_port').val();
                var casb = new OpswatCASB();
                if(isV3) {
                    casb.jsonp({
                    'serverPort': server_port,
                    'callback' : myCallback,
                    'apiUrl' : '/opswat/3/devinfo',
                    'sessionId' : sessionId
                    });
                } else {
                    casb.jsonp({
                        'serverPort': server_port,
                        'callback' : myCallback,
                        'sessionId' : sessionId
                    });
                }
            }

            function uuidv4() {
              return ([1e7]+-1e3+-4e3+-8e3+-1e11).replace(/[018]/g, c =>
                (c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> c / 4).toString(16)
              );
            }
    </script>
    </body>
</html>
```

Note: you can find **jquery-3.1.1.min.js**, jsrsasign-all-min.js and **opswat.jsonp.js** in the [*client_sample_code_v3.zip*](https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/client_sample_code_v3.zip)** **

**Success response:**

```plaintext
{
  "code": 0,
  "description": "Success",
  "info": {
    "hwid": "7EF012F7AB8E454FA37B0D2E9A2E812C"
  }
}
```

**Error response:**

```plaintext
{
    "code": -41,
    "description": "Hardware ID failed to get"
}
```

## Support chart

As of November 10th, 2016, Cross-Domain API solution is only supported on persistent agents.

|  | Persistent agent | On-demand agent |
| ---- | ---- | ---- |
| Windows | Yes | Yes |
| macOS | Yes | Yes |
| Linux | Yes |  |
| Android | No |  |
| iOS | No |  |

The below MetaDefender Endpoint versions support https protocol for the cross-domain API.

- Windows persistent agent version: 7.6.121.0+
- macOS persistent agent version: 10.4.147.0+

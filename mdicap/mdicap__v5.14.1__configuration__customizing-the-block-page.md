<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/configuration/customizing-the-block-page -->

# Block Page Customization and Configuration

By design, whenever a request is blocked for some reason, then a block page will be returned back from MetaDefender ICAP Server to client side as follows (the actual blocking reason message may differ):

MetaDefender ICAP Server supports users to create their own custom block page, and overwrite the default one.

## [Replacing the default block page](/docs/mdicap/v5.14.1/configuration/customizing-the-block-page#replacing-the-default-block-page)

There are two options: either using UI configurations (recommended) or using legacy file overwritten on disk.

### [Replacing via UI configurations (recommended)](/docs/mdicap/v5.14.1/configuration/customizing-the-block-page#replacing-via-ui-configurations-recommended)

Info

From MD ICAP Server v5.4.0, custom block page can be managed via the UI and able to assign individual custom block page to specific workflow

#### [Block page management (Under Inventory)](/docs/mdicap/v5.14.1/configuration/customizing-the-block-page#block-page-management-under-inventory)

Go to **Library → Block Pages**

Manage your custom block page(s), and also track which workflow that that custom block page is assigned to.

Info

Custom block page content will be encoded with base64, the maximum length (after encoded) is 10000 bytes.

#### [Assign block page to work flow](/docs/mdicap/v5.14.1/configuration/customizing-the-block-page#assign-block-page-to-work-flow)

Go to **Workflows** **→** Select the workflow -> go to **Block Page** tab

**Block Page Options:**

- **Default**: the MetaDefender ICAP Server default block page will be applied to the workflow

  - Note: Just in case the default block page has already overwritten via [Replacing via Legacy method](/docs/mdicap/v5.14.1/configuration/customizing-the-block-page#replacing-via-legacy-method) then the HTML file stored in path <Installation folder>\data\block_page.html will be used as default block page

- **Custom**: Select the custom block page (can be managed / modified under Inventory - Block Pages) to assign that workflow.

- **Redirect to a URL**: the pre-defined data (using with placeholders via query parameters or path parameter) will be sent to a designated URL location for processing.

For instance, following setting will send block file name info to some host via query parameters for processing.

**Adding Placeholder**

- Beside [Additional placeholders](/docs/mdicap/v5.14.1/configuration/customizing-the-block-page#additional-placeholders), additional placeholder can be added (if the header is not found then the default value will be filled up (default value can put blank value).

  - REQMOD: the HTTP header is getting from request header.
  - RESPMOD: the HTTP Header is getting from response header.
- Maximum custom place holder: 10.
- Max length of HTTP header: 64.
- Max length of default value: 512.

### [Replacing via Legacy method](/docs/mdicap/v5.14.1/configuration/customizing-the-block-page#replacing-via-legacy-method)

To replace the default block page create a HTML file with the custom content according to the following:

| Operating system | Path | Default path | Owner | Permissions |
| --- | --- | --- | --- | --- |
| Windows or Windows Server | <Installation folder>\data\block_page.html | C:\Program Files\OPSWAT\Metadefender ICAP Server\data\block_page.html | Local Service | Read |
| Linux (RHEL / CentOS / Debian / Ubuntu) | <Data folder>block_page.html | /var/lib/mdicapsrv/block_page.html | mdicapsrv:mdicapsrv | r-- (400) |

Note

The default block page is not represented as a file in the file system. If the above file exists, then the default block page is overridden.

## [ICAP Server block messages](/docs/mdicap/v5.14.1/configuration/customizing-the-block-page#icap-server-block-messages)

To display ICAP Server block messages in the custom page include the following token at the desired position in the page:

%%%icap_block_message%%%

This token will be replaced by the appropriate ICAP Server block message.

## [Additional placeholders](/docs/mdicap/v5.14.1/configuration/customizing-the-block-page#additional-placeholders)

For custom block pages several additional placeholder tokens are also supported.

Note

The placeholder tokens below are not used in the default block page, but are available for a custom block page.

| Placeholder | Description | Note |
| --- | --- | --- |
| %%%url%% | URL parsed from the original HTTP request. |  |
| %%%client_ip%%% | Address of the client from whom the request originated. |  |
| %%%server_name%%% | Name of the server the ICAP Server is running on. |  |
| %%%timestamp%%% | Arrival of the request to the ICAP Server. |  |
| %%%filenames%%% | Filenames which are blocked. | Present only if some violations were found, otherwise replaced by empty string. |
| %%%mimes%%% | Media types for blocked files. | Present only if some violations were found, otherwise replaced by empty string. |
| %%%violations%%% | Violations for blocked files. | Present only if some violations were found, otherwise replaced by empty string. |
| %%%violations_short%%% | The first violation for the blocked file. | Present only if some violations were found, otherwise replaced by empty string. |

### [Example](/docs/mdicap/v5.14.1/configuration/customizing-the-block-page#example)

The following example is the source code of a simple custom page that displays the ICAP Server messages only with no formatting at all:

<!doctype html>
<html>
<body>
%%%icap_block_message%%%
</body>
</html>

It renders a very simple page that looks like this:

## [Default block page source code](/docs/mdicap/v5.14.1/configuration/customizing-the-block-page#default-block-page-source-code)

The default lock page's source code can be reused to create a customized one.

Default block page source code
<!doctype html>
<html lang="en">
<head>
<title>MetaDefender ICAP server - File blocked</title>
<link href="https://fonts.googleapis.com/css?family=Roboto:400,500" rel="stylesheet">
<style>
html, body { margin: 0; font-size: 14px; position: relative; height: 100%; background-color: #F9F9F8; color: #273238; font-family: 'Roboto', sans-serif; }
a { color: inherit; }
a:hover { color: inherit; }
hr { margin: 0; border: 0; border-top: 1px solid #EFEFED; }
.box { margin: 30px; width: 678px; padding: 30px; background-color: #FFFFFF; border: 1px solid #EFEFED; box-shadow: 0 0 20px 0 #EFEFED; }
.box .title { margin-top: 0; color: #2672FB; font-weight: 500; }
.box .message { margin: 30px 0; }
.box .metascan { margin-top: 30px; font-size: 80%; color: #5F6C88; }
#container { display: flex; justify-content: center; align-items: center; height: 100%; }
</style>
<meta charset="UTF-8">
</head>
<body>
<div id="container">
<div class="box">
<h1 class="title">File blocked</h1>
<p class="message">%%%icap_block_message%%%</p>
<hr>
<div class="metascan">Your administrator is using OPSWAT’s <a href="https://www.opswat.com/products/metadefender" target="_blank">MetaDefender Core technology</a> to scan downloads with multiple anti-malware engines. See additional ways MetaDefender Core can be used by trying the <a href="https://www.opswat.com/products/metadefender/client" target="_blank">MetaDefender Client</a> demo for scanning endpoint processes and files or the <a href="https://metadefender.opswat.com/" target="_blank">metadefender.opswat.com</a> file scanning service.</div>
</div>
</div>
</body>
</html>

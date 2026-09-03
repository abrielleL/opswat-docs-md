<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/configuration/user-interface-customization -->

# User interface customization

## [Graphical user interface](/docs/mdemail/6.4.1/configuration/user-interface-customization#graphical-user-interface)

In **Settings > Rebranding** different parts of the GUI can be rebranded with customized images and text. Currently the following GUI parts are supported

1. Rescan page: page of quarantine actions that are available as [quarantine report or notification email actions](/docs/mdemail/6.4.1/operating/quarantine-reports#supported-functions).

### [Customization](/docs/mdemail/6.4.1/configuration/user-interface-customization#customization)

To change a GUI element, hover over it with the mouse. If changing the element is supported, then the GUI element gets a blue box:

#### [Image elements](/docs/mdemail/6.4.1/configuration/user-interface-customization#image-elements)

Images can be replaced or hidden. An uploaded image is resized automatically to fit its container. Uploaded images must be less than 5MBs.

Propagation delay

In shared database setups, images set on one instance are distributed to other instances in every 10 minutes potentially causing delay for customized GUIs on other instances.

SVG sanitization

To address some security risks, Email Gateway Security removes `<script>` elements from `.svg` files when uploaded.

#### [Text elements](/docs/mdemail/6.4.1/configuration/user-interface-customization#text-elements)

Only the text string can be customized. The text formatting (e.g. weight) comes from the default design.

Translations

Translations are supported through the GUI for the locales that are defined for the product. For details see [Translation](/docs/mdemail/6.4.1/configuration/translation-support#translation).

To show the translated version of the GUI part, select the appropriate locale from the *Language* dropdown.

#### [HTML elements](/docs/mdemail/6.4.1/configuration/user-interface-customization#html-elements)

For certain elements (that typically require more complex customization) a WYSWYG/HTML editor is supported.

HTML source

To view and edit the HTML source of the element, click the `</>` button.

#### [Restore to default](/docs/mdemail/6.4.1/configuration/user-interface-customization#restore-to-default)

Each individual GUI element or the GUI part as a whole can be restored to the default.

## [Alert, notification and quarantine report emails](/docs/mdemail/6.4.1/configuration/user-interface-customization#alert-notification-and-quarantine-report-emails)

By default, alert, notification and quarantine report emails have an OPSWAT styling (colors, logos, texts). The default templates of these emails are stored as xslt templates. If the text or the style of the alert, notification and quarantine report emails need to be changed, the appropriate xslt template needs to be edited.

### [Overview](/docs/mdemail/6.4.1/configuration/user-interface-customization#overview)

Templates of the notification, alert and report emails can be found in:

<installation directory>\mailagenthost\xslt

Default:

C:\Program Files\OPSWAT\MetaDefender Email Security\mailagenthost\xslt

These files are plain text `xslt` (Extensible Stylesheet Language Transformations) files, that can be edited using plain text editors or xslt editors.

Content and structure of the xslt templates can be changed to customize the alert, notification and quarantine report emails.

### [Per-rule blocked notification templates](/docs/mdemail/6.4.1/configuration/user-interface-customization#per-rule-blocked-notification-templates)

[Security Rules](/docs/mdemail/6.4.1/configuration/policy) allow administrators to assign custom blocked notifications to each security rule under *Advanced Threat Prevention*.

To create a custom notification template, follow these steps:

1. **Start from the built-in template.** Copy the default blocked notification file `notification_blocked.default.xsl` from the `xslt` folder as your starting point:
2. **Name the new file** using the pattern `notification_blocked.<variant>.xsl`, where `<variant>` is a short, descriptive name of your choice (e.g., `vip`, `finance`). Example: `notification_blocked.vip.xsl`.
3. **Place the file** in the installation `xslt` folder: `<installation directory>\mailagenthost\xslt\` Default: `C:\Program Files\OPSWAT\MetaDefender Email Security\mailagenthost\xslt\`

**Select the variant in the security rule.** After placing the file, the variant name (e.g., `vip`) becomes available in the notification template dropdown of any security rule. No service restart is required — the `xslt` folder is scanned dynamically. For details see the *Advanced Threat Prevention* subsection under [Security policy.](/docs/mdemail/6.4.1/configuration/policy#security-policy)

### [Examples](/docs/mdemail/6.4.1/configuration/user-interface-customization#examples)

The template for blocked notifications can be found in the *notification_blocked.xsl* file. It is an XSLT file which contains HTML, CSS and XSLT elements. By modifying the HTML and CSS elements you can get a different look or language for your notifications. XSLT elements **should not be modified** as we use them to fill the email with actual data.

By default, the blocked notification email looks like below. In the following examples we will customize this.

#### [Replacing the logo](/docs/mdemail/6.4.1/configuration/user-interface-customization#replacing-the-logo)

In order to replace the logo the appropriate image reference should be found and modified in the *notification_blocked.xsl* file:

Original logoCopy<a href="https://www.opswat.com/products/metadefender/email-security">
<img src="img/logo.png" />
</a>

The new logo is placed as *newlogo.png* image in the *img* folder. In this case we should modify this part to look like this:

Modified logoCopy<a href="https://www.opswat.com/products/metadefender/email-security">
<img src="img/newlogo.png" />
</a>

After this modification the notification email will look like this:

#### [Customizing colors](/docs/mdemail/6.4.1/configuration/user-interface-customization#customizing-colors)

To customize the colors of the table containing the information related to the blocked email modify this part in the *style* block of the xslt template:

Original colorsCopytable.email-details .table-header { background: #2672FB; color: #FFFFFF; }
table.email-details .table-header p {font-weight: 700; white-space: nowrap;}
table.email-details tr.alt td { background: #EAEFF2; }
table.email-details tr.alt .table-header { background: #2672FB; }Modified colorsCopytable.email-details .table-header { background: #4e6691; color: #FFFFFF; }
table.email-details .table-header p {font-weight: 700; white-space: nowrap;}
table.email-details tr.alt td { background: #b1d8ef; }
table.email-details tr.alt .table-header { background: #4e6691; }

After this modification the notification email will look like this:

#### [Removing blocks](/docs/mdemail/6.4.1/configuration/user-interface-customization#removing-blocks)

Information may be missing

Removing xslt elements may give unexpected results (e.g. information missing from the email).

To remove the *Scan result* link row from the notification email, the following part needs to be removed from the *notification___blocked*_.xsl_ template:

HtmlCopy<tr class="alt">
<td class="table-header">
<p>Scan result:</p>
</td>
<td>
<p>
<xsl:for-each select="scan_result_links/result_link">
<xsl:element name="a">
<xsl:attribute name="href">
<xsl:value-of select="url" />
</xsl:attribute>
<xsl:value-of select="result_filename" />
</xsl:element>
<br/>
</xsl:for-each>
</p>
</td>
</tr>

After this modification the notification email will look like this without the scan result row:

<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/advanced-deployment/disclaimer-screen-customization -->

# Disclaimer Screen Customization

View as Markdown Ask ChatGPT about this page Ask Claude about this page

As default setting, the disclaimer screen at the beginning will show the OPSWAT's EULA (End-User License Agreement) in English.

To change content of this screen to specific languages, create and upload your own customized disclaimer file at `Edit language` configuration page.

Image: "Upload Disclaimer" option on Kiosk configuration page

The reference disclaimer file can be found at following file directory on Windows: `C:\Program Files (x86)\OPSWAT\Metadefender Kiosk\Client\en\resources\disclaimers\disclaimer.html` .

You can also create your own customized disclaimer file following this guideline:

- File format is .html
- You can only use limited HTML Elements only, with heading `<h>`, paragraph `<p>` and line break `<br>` tags

For example:

HtmlCopy<h6>Heading 1</h6>
<p>Paragraph 1</p>
<br/>
<h6>Heading 2</h6>
<p>Paragraph 2</p>

If disclaimer file is valid and uploaded successfully, it will be shown in `Upload Disclaimer` value with the name following the format `disclaimer_{lang_id}.html`

Image: Click Browse to upload your Disclaimer file

The corresponding HTML file will be also added to the same folder directory of the reference file.

Info

- Default EULA will be shown if there is no disclaimer.html or valid customized disclaimer file of a specific language in the disclaimer folder.
- Customized disclaimer files will be kept during upgrading Kiosk.
- From verion 4.6.7, customized disclaimer files will be included in the backup configuration settings archive to restore disclaimer settings on this or a different Kiosk system.

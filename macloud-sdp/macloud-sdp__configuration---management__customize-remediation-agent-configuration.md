<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/customize-remediation-agent-configuration -->

# Customize Remediation Agent Configuration

The examples in this document is using Windows. Be sure to make changes according to the targeted operating system. For more information on how to obtain a rebranding package, please go to [Rebranding Package](/docs/macloud-sdp/configuration---management/customize-remediation-page) .

### [Hide Download Button](/docs/macloud-sdp/configuration---management/customize-remediation-agent-configuration#hide-download-button)

To hide the download button on your remediation page, please insert the following generic.json file under the "download_button" section for the targeted operating system:

JsonCopy"windows": {
"template": "",
"group_id": ""
}
### [Download Persistent MetaDefender Endpoint](/docs/macloud-sdp/configuration---management/customize-remediation-agent-configuration#download-persistent-metadefender-endpoint)

To prompt the end-users to install the Persistent MetaDefender Endpoint on your remediation page, please insert the following generic.json file under the `"download_button"` section for the targeted operating system:

JsonCopy"windows": {
"template": "<p><a target='_blank' class='gray-button m-l-none' href='%download_windows_persistent%'>DOWNLOAD OPSWAT Client</a></p><div class='is-hidden'><p>%os_name%</p><p><a target='_blank' href='%download_other_links%'>Download an installer for other operating systems</a></p></div>",
"group_id": "<enter-group-id>"
}

Once completed, save the JSON file.

### [Download On-Demand Limited MetaDefender Endpoint](/docs/macloud-sdp/configuration---management/customize-remediation-agent-configuration#download-on-demand-limited-metadefender-endpoint)

To prompt the end-users to install the On-Demand MetaDefender Endpoint on your remediation page, please insert the following generic.json file and update the `"download_button"` section for the targeted operating system:

JsonCopy"windows": {
"template": "<p><a target='_blank' class='gray-button m-l-none' href='%download_windows_ondemand%'>DOWNLOAD OPSWAT Client</a></p><div class='is-hidden'><p>%os_name%</p><p><a target='_blank' href='%download_other_links%'>Download an installer for other operating systems</a></p></div>",
"group_id": "<enter group-id>"
}

Once completed, save the JSON file.

### [Download On-Demand Limited MetaDefender Endpoint](/docs/macloud-sdp/configuration---management/customize-remediation-agent-configuration#download-on-demand-limited-metadefender-endpoint)

To prompt the end-users to install the on-demand limited MetaDefender Endpoint on your remediation page, please insert the following generic.json file and update the `"download_button"` section for the targeted operating system:

JsonCopy"windows": {
"template": "<p><a target='_blank' class='gray-button m-l-none' href='%download_windows_limited%'>DOWNLOAD OPSWAT Client</a></p><div class='is-hidden'><p>%os_name%</p><p><a target='_blank' href='%download_other_links%'>Download an installer for other operating systems</a></p></div>",
"group_id": "<enter group-id>"
}

Once completed, save the JSON file.

### [Additional Information](/docs/macloud-sdp/configuration---management/customize-remediation-agent-configuration#additional-information)

- **Android** : download button template for android device
- **iOS** : download button template for android device
- **group_id** : Group IDs can be obtained by going to **Inventory > Device Groups > Select device group > Settings > Group ID**. You can then take the ID and place it in your JSON between quotation marks.

When the desired changes are complete, upload your rebranding package into MetaDefender IT Access for the changes to take affect.

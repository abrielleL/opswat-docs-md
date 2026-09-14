<!-- source: https://www.opswat.com/docs/cm/configurations/customize-remediation-agent-configuration -->

# Customize Remediation Agent Configuration

> **Info**
>
> The examples in this document is using Windows. Be sure to make changes according to the targeted operating system. For more information on how to obtain a rebranding package, please go to [Rebranding Package](https://www.opswat.com/docs/cm/configurations/rebranding-package).

### Hide Download Button

To hide the download button on your remediation page, please insert the following generic.json file under the "download_button" section for the targeted operating system:

```json
"windows": {
            "template": "",
            "group_id": ""
        }
```

### Download Persistent MetaDefender Endpoint

To  prompt the end-users to install the Persistent MetaDefender Endpoint on your remediation page, please insert the following generic.json file under the `"download_button"` section for the targeted operating system:

```json
"windows": {
      "template": "<p><a target='_blank' class='gray-button m-l-none' href='%download_windows_persistent%'>DOWNLOAD OPSWAT Client</a></p><div class='is-hidden'><p>%os_name%</p><p><a target='_blank' href='%download_other_links%'>Download an installer for other operating systems</a></p></div>",
      "group_id": "<enter-group-id>"
    }
```

Once completed, save the JSON file.

### Download On-Demand Limited MetaDefender Endpoint

To prompt the end-users to install the On-Demand MetaDefender Endpoint on your remediation page, please insert the following generic.json file and update the `"download_button"` section for the targeted operating system:

```json
"windows": {
      "template": "<p><a target='_blank' class='gray-button m-l-none' href='%download_windows_ondemand%'>DOWNLOAD OPSWAT Client</a></p><div class='is-hidden'><p>%os_name%</p><p><a target='_blank' href='%download_other_links%'>Download an installer for other operating systems</a></p></div>",
      "group_id": "<enter group-id>"
    }
```

Once completed, save the JSON file.

### Download On-Demand Limited MetaDefender Endpoint

To prompt the end-users to install the on-demand limited MetaDefender Endpoint on your remediation page, please insert the following generic.json file and update the `"download_button"` section for the targeted operating system:

```json
"windows": {
"template": "<p><a target='_blank' class='gray-button m-l-none' href='%download_windows_limited%'>DOWNLOAD OPSWAT Client</a></p><div class='is-hidden'><p>%os_name%</p><p><a target='_blank' href='%download_other_links%'>Download an installer for other operating systems</a></p></div>",
"group_id": "<enter group-id>"
}
```

Once completed, save the JSON file.

### Additional Information

- **Android**  : download button template for android device
- **iOS** : download button template for android device
- **group_id** : Group IDs can be obtained by going to **Inventory > Groups > Open Endpoint Group > Settings > Group ID**. You can then take the ID and place it in your JSON between quotation marks.

![](https://uploads.developerhub.io/prod/97qW/fkeqa1d44lxdh7ky4v86fp7suoouuopmac9io8f9cuc3xj1wj8b1znj173b2s726.png)

When the desired changes are complete, upload your rebranding package into My OPSWAT Central Management for the changes to take affect.

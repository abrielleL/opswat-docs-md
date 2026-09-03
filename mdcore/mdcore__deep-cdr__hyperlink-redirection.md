<!-- source: https://www.opswat.com/docs/mdcore/deep-cdr/hyperlink-redirection -->

# Hyperlink redirection

This option is a good choice when you have a redirection service. Deep CDR will add a prefix hyperlink to current hyperlinks. When the user clicks on a hyperlink, your inspection service will scan the link and redirect them to the original URL.

This is an example when integrating with [MetaDefender Cloud Safe URL Redirect](https://www.opswat.com/docs/mdcloud/operation/safe-url-redirect):

Original: "Please click [here](https://www.opswat.com/) to contact us"

Sanitized: "Please click [here](http://metadefender.opswat.com/safe-redirect/https%3A%2F%2Fwww.opswat.com) to contact us"

## [Dynamic hyperlink redirection](/docs/mdcore/deep-cdr/hyperlink-redirection#dynamic-hyperlink-redirection)

The feature Dynamic hyperlink redirection allows users to pass a `container_identifier` via `engines-metadata` to generate dynamic URL output.

Container identifier serves as an identifier of container document of hyperlinks. Clients may leverage for their own purposes.

### [Supported file formats](/docs/mdcore/deep-cdr/hyperlink-redirection#supported-file-formats)

This feature applies to **HTML**, **TXT**, and **RTF** file formats only.

### [Configuration](/docs/mdcore/deep-cdr/hyperlink-redirection#configuration)

Configuration: **Workflow > [Workflow Name] > Deep CDR > Advanced Configuration > Others > HTML**, then:

- **Process Hyperlink Behavior:** Select how hyperlinks should be processed. Set this to **Add hyperlink prefix**.
- **Hyperlink Prefix:** Define the prefix that will be added to output hyperlinks in HTML. To use the feature, the hyperlink prefix must include two placeholders: `encoded_target_url` and `container_identifier` , e.g., `https://metadefender.opswat.com/safe-redirect?target=<encoded_target_url>&dataid=<container_identifier>`.

Now we can pass `container_identifier` via the `engines-metadata` (see [Supported engines-metadata JSON](https://www.opswat.com/docs/mdcore/v5.18.0/deep-cdr/supported-engines-metadata-json)) to generate dynamic output URL.

Alternatively, we can pass `hyperlink_prefix` with placeholder `<encoded_target_url>` and pre-inserted `container_identifier`. This setting takes a higher priority over the workflow setting. `hyperlink_prefix` should come along with a setting section name of a corresponding file format. Below is the list of setting sections.

| File format | Setting section name |
| --- | --- |
| HTML | html2html |
| TXT | txt2txt |
| RTF | rtf2rtf |

JsonCopy{
"deep_cdr": {
"container_identifier": "69aab91a5e37baa713442af9"
}
}JsonCopy{
"deep_cdr": {
"html2html.hyperlink_prefix": "https://metadefender.opswat.com/safe-redirect?target=<encoded_target_url>&dataid=69aab91a5e37baa713442af9"
}
}
### [Example](/docs/mdcore/deep-cdr/hyperlink-redirection#example)

With an extracted hyperlink from a document, `https://www.opswat.com/docs`, the output URL will be `https://metadefender.opswat.com/safe-redirect?target=https%3A%2F%2Fwww.opswat.com%2Fdocs&dataid=69aab91a5e37baa713442af9` .

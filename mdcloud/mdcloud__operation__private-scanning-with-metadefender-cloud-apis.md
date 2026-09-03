<!-- source: https://www.opswat.com/docs/mdcloud/operation/private-scanning-with-metadefender-cloud-apis -->

# Private Scanning and Private Processing with MetaDefender Cloud APIs

By submitting a file to MetaDefender Cloud you are giving OPSWAT permission to share the results of your submission with the cyber security community;

(a) you give OPSWAT permission to share the results of your submission with the cybersecurity community;

(b) you consent to OPSWAT sharing any executables you submit with third-party malware exchange partners for the purpose of such partners improving their anti-malware products;

(c) you agree to our [Terms of Service](https://www.opswat.com/legal/free-tools-terms-of-use) and [Privacy Policy](https://www.opswat.com/legal/privacy-policy). Please do not submit any personal data to OPSWAT.

For all its standard, professional and enterprise users, MetaDefender Cloud provides the ability to scan files privately. This **private scanning** feature is available through the MetaDefender Cloud APIs, metadefender.opswat.com website and the MetaDefender Chrome Extension. All files scanned in private mode are not stored or shared, although scan results will remain available in the MetaDefender Cloud database.

During the file processing, the given file has to be stored in temporary storage by MetaDefender Cloud. After the completion of the scanning process, the scan result is stored in the database and the file is permanently removed from our storage to ensure the privacy of our customers.

## [How to Perform an API Request with Private Scanning](/docs/mdcloud/operation/private-scanning-with-metadefender-cloud-apis#how-to-perform-an-api-request-with-private-scanning)

In order to use the private scanning feature, clients have to send all requests on POST /v4/file endpoint with header `samplesharing`. This flag is only available to users who have a paid license for MetaDefender Cloud. Please view our [POST - Analyze file](https://docs.opswat.com/mdcloud/metadefender-cloud-api-v4#file-upload) API documentation for further information, and look after `samplesharing` header.

var request = require('request');
var fs = require("fs");
 
var formData = {
file: fs.createReadStream(__dirname + '/file')
};
 
request.post({
url: 'https://api.metadefender.com/v4/file',
formData: formData,
headers: {
apikey: process.env.APIKEY,
samplesharing: 0
}
},
function(err, httpResponse, body) {
if (err) {
return console.error('upload failed:', err);
}
console.log(body);
}
);
## [Private Scanning from the UI](/docs/mdcloud/operation/private-scanning-with-metadefender-cloud-apis#private-scanning-from-the-ui)

Logged in users with paid accounts can enable the Private processing option from the advanced upload section.

## [Private Processing](/docs/mdcloud/operation/private-scanning-with-metadefender-cloud-apis#private-processing)

To provide our customers with an additional level of privacy, we offer **private processing** in addition to private scanning. When `privateProcessing`is set to 1, this feature will not only immediately remove files after analysis is done, but also ensure that the results of those scans will only be available to the owner who submitted the files for scanning in the first place (only with the same API Key). This applies to all file processing results including: multiscanning, sandbox, dlp. If private processing is enabled, the customer can't fetch sandbox scan results, only with the same API Key which was used to submit the files for scanning. Using Private processing, the scan result won't be added in hash collection. Private processing scan results can't be retrieved using hash look-up.

## [Data Sanitization](/docs/mdcloud/operation/private-scanning-with-metadefender-cloud-apis#data-sanitization)

When uploading files in private mode and requesting to run Deep CDR, the sanitized version of the file will be available to download from our servers for 24 hours. After 24 hours, the sanitized version of the file is deleted automatically to ensure privacy for our customers. Sanitized files can also be removed on demand by using the [Delete Sanitized version of the file](https://docs.opswat.com/mdcloud/metadefender-cloud-api-v4#deletedelete-the-sanitized-version-of-the-file) endpoint.

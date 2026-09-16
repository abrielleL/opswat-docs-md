<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-do-we-utilize-api-uploads-so-the-correct-file-type-and-sanit -->

# How do we utilize API uploads so the correct file type and sanitization occurs every time?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

Use the ‘binary’ upload method when sending files to Core for scanning via API. If you add files to the body of a ‘Post’ API call using another method such as ‘form-data’, the content of the file that our Core server receives gets modified. This can result in our system incorrectly identifying the file type and being unable to fully sanitize the files. The ‘binary’ method is the only supported method for attaching files to the body of a ‘Post’ API call.

## [Example using Postman:](/docs/mdcore/v5.22.0/knowledge-base/how-do-we-utilize-api-uploads-so-the-correct-file-type-and-sanit#example-using-postman)

1. Press the + Button at the top of the Postman tool to begin a new API request.
2. Select ‘Post’ as the call type from the drop down menu

3. Enter the full URL for your MetaDefender Core server’s API interface.

4. Add any optional headers outlined in [POST - Analyze File (Asynchronous mode)](/docs/mdcore/v5.22.0/metadefender-core#fileanalysispost). Below, I will use the ‘apikey’ header

5. Change to the body of the API call and select ‘binary’ as your upload type.
6. Select your file by pressing the + button and browsing to the file you would like scanned

7. Press Send.

If the scan was successful, you should receive a server response of ‘200’ along with the data_id associated with the file scan.

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).

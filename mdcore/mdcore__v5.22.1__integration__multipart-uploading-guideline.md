<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/integration/multipart-uploading-guideline -->

# Multipart upload guideline

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Introduction](/docs/mdcore/v5.22.1/integration/multipart-uploading-guideline#introduction)

Since version 5.11.0, MetaDefender Core introduces a brand - new API that accepts individual requests containing parts split from a file and automatically combines them into the original file for scanning. The new API best fits one of the following use cases.

- If you have a stable, high-bandwidth network, you can split a large file into multiple parts on your end and call the new API to upload the parts simultaneously to maximize the available bandwidth.
- If there are size limits on uploaded files, you can divide a large file into smaller parts that fit within those limits and use the API to upload them separately to MetaDefender Core.
- If the network is unstable, a file upload can easily be interrupted in the middle. Instead of uploading entire file again, the API can be used to upload only the interrupted parts.

In all cases mentioned above, once the parts are fully uploaded, MetaDefender Core combines them into the original file and begins scanning it with the selected workflow.

This feature composes a set of following APIs

| Functionality | API |
| --- | --- |
| Initiate multipart upload session | POST `/file/multipart` |
| Upload individual part to multipart upload session | POST `/file/multipart/{data_id}` |
| Fetch status of multipart upload session | GET `/file/multipart/{data_id}` |
| Abort multipart upload session | DELETE `/file/multipart/{data_id}` |

## [How to enable](/docs/mdcore/v5.22.1/integration/multipart-uploading-guideline#how-to-enable)

Multipart upload is disabled by default. To enable it, please follow these steps

1. Log in to MetaDefender Core dashboard with your account
2. Expand `Workflow Management` --> `Workflows` in the left sidebar, and select the workflow to be affected.
3. In `General` tab, navigate to `Multipart Uploading` section and tick to `Enable file uploaded by multiple parts simultaneously`.
4. Hit `Save changes` to apply the new setting.

## [How to use](/docs/mdcore/v5.22.1/integration/multipart-uploading-guideline#how-to-use)

You can use the new APIs in your applications in three steps

1. Initiate a new multipart upload session in MetaDefender Core.
2. Split the file for scanning into multiple parts on your end.
3. Upload the parts into the created multipart upload session in MetaDefender Core.

For the first step, you need create a new multipart upload session by making a POST`/file/multipart` request to MetaDefender Core. The request contains no body but must include an essential header, `total-length`, which indicates the size of the entire uploaded file in bytes. For a full list of supported headers, please access [here](https://docs.opswat.com/mdcore/metadefender-core#createmultipartuploadpost).

If successful, HTTP code 200 OK and `data_id` will be returned. You should keep `data_id` for the next commands, such as uploading parts to the session, checking the upload status, aborting the upload session and checking the scan status.

In the second step, you should split the submitted file into multiple parts that fit your needs and size limitations.

In the final step, you should make several multipart upload requests to MetaDefender Core via POST`/file/multipart/{data_id`}. Each request carries one of the parts split from the original file. `data_id` term in the API is the output of the first step.

Info

APIPOST`/file/multipart/{data_id}` can only accept requests whose `content-type` header is set to `application/octet-stream` ; otherwise, the request body is ill-formatted and resulting in error HTTP 400 BAD REQUEST .

The multipart upload request needs both the offset and length of the uploaded part, which must be provided by the `content-range` header in the form of `offset-length/total`, where the `offset` indicates the position from the beginning of the file to the first byte of the part. `length` and `total` are, respectively, the part size and the total size of the entire file, all in bytes .

Suppose you split a file of 10,485,760 bytes (10 MB) into 3 parts; then `content-range` header of each request should be 0-2000000/10485760, 2000000-2000000/10485760, and 4000000-6485760/10485760, respectively. You can find further details about the API [here](https://www.opswat.com/docs/mdcore/metadefender-core#uploadpartpost).

When all parts are fully uploaded, MetaDefender Core will automatically combine them into a complete file and begin scanning it with the selected workflow. You can later fetch the scan progress and result using the traditional API POST `/file/{data_id}`, or you can cancel file processing with POST `/file/{data_id}/cancel`.

If the network is broken while one of the parts is being uploaded, you can make another POST `/file/multipart/{data_id`} request to upload just the interrupted part again to MetaDefender Core. You can also apply the same approach if your application crashes while uploading parts or MetaDefender Core service is interrupted due to upgrade or maintenance.

With split parts, depending on your network bandwidth, you can choose to upload them one by one, several at a time, or all of them simultaneously to MetaDefender Core. Additionally, except for the first and the last parts, the content range of a part can overlap with its next or previous ones without causing any confusion to MetaDefender Core.

At any time, you can fetch the upload status with GET `/file/multipart/{data_id`} or abort part uploads totally with DELETE `/file/multipart/{data_id`}. As soon as the abort request is received, MetaDefender Core will stop all requests uploading parts and return HTTP code 422 CANCED. The multipart upload session is then set to `CANCELED` verdict and all resources consumed by the session thus far are released.

JsonCopy{
"err": "Multipart uploading session cancelled"
}
## [How to configure](/docs/mdcore/v5.22.1/integration/multipart-uploading-guideline#how-to-configure)

By default, a multipart upload session, once initiated successfully, will be available for parts uploaded within 60 minutes. Outside that duration, HTTP code 409 CONFLICT is returned for each call to POST`/file/multipart/{data_id}`.

JsonCopy{
"err": "Multipart uploading session timed out"
}

You can extend or collapse the time range as needed by following these steps:

1. Login to MetaDefender Core dashboard with your admin account.
2. Expand `Workflow Management` --> `Workflows` on the left sidebar.
3. Select the workflow of interest.
4. In `General` tab, navigate to `Multipart uploading` section.
5. Modify `Time for parts to live` to your desired value.

By definition, MetaDefender Core stores files that are submitted by multipart upload in `<Install-directory>/data/multipart` on Windows and `/var/lib/ometascan/multipart` on Linux. You can modify the location to another according to your needs.

- On Windows, run Registry Editor, navigate to `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\global`, add a new string named `multipartpath`, fill in the path to new location, and hit OK to complete. Restart MetaDefender Core to apply the new setting.

- On Linux, open file `/etc/ometascan/ometascan.conf` in edit mode. Under `[global]` session, add a new item named `multipartpath`, fill in the path to new location, and save the file. Restart MetaDefender Core to apply the new setting.

Warning

Please ensure that MD Core has the necessary permission to access the files in the new folder.

## [Multipart upload and other facilities](/docs/mdcore/v5.22.1/integration/multipart-uploading-guideline#multipart-upload-and-other-facilities)

When all parts of a file are uploaded fully to MetaDefender Core, you can cancel the file processing with POST POST `/file/{data_id}/cancel`. Please do not be confused by the two APIs. DELETE `/file/multipart/{data_id`} is used when parts of the file are being uploaded, while POST `/file/{data_id}/cancel` is the best match for cases when the file content is fully received and the processing is underway.

API POST `/file/multipart` supports `callbackurl` header which specified the URL of an external web server to which MetaDefender Core sends the analysis result as soon as the file processing is complete. Header `sanitizedurl` is also supported. The header provides the URL of an external web server that will receive the file content sanitized and/or processed by MetaDefender Core from the original.

A file that is uploaded by multiple parts can be linked to a specific batch. To do this, please fill `batch_id` of the batch in `batch` header of POST`/file/multipart` request to MetaDefender Core. An HTTP code 200 OK and returned `data_id` implies that the file is successfully linked to the batch. The batch cannot be closed until all its linked files are fully uploaded.

Time availability feature under Quality of Service can be applied to files submitted via multipart upload. As long as the multipart upload session is initiated within the time availability, it remains valid for uploaded parts, event if they are uploaded outside the time range. Even so, those parts ust remain within the time-for-parts-tove.

## [Multipart upload and load balancing](/docs/mdcore/v5.22.1/integration/multipart-uploading-guideline#multipart-upload-and-load-balancing)

In many deployment scenarios, a number of MetaDefender Core instances are placed behind a load balancer to share the workload. Multipart upload can also be utilized in these scenarios. For this feature to function correctly, a load balancer sticky session must be used in your application to ensure that all parts of a file are uploaded to the same session which is owned by one of the instances behind the load balancer. You can read more about sticky session for load balancing [here](https://docs.opswat.com/mdcore/installation/using-external-load-balancer#sticky-session-load-balancing).

From your application's perspective, you can follow these steps:

1. Make a POST`/file/multipart` request to the load balancer **without cookies**.
2. Keep the cookies and `data_id` returned by the load balancer for subsequent calls.
3. Make POST `/file/multipart/{data_id`} requests with the cookies received in step 2 for every uploaded part.

## [Considerations](/docs/mdcore/v5.22.1/integration/multipart-uploading-guideline#considerations)

- Multipart upload does not support `downloadfrom` header.
- MetaDefender Core can only recover the upload of parts but not the processing of a file if it has already been fully combined.
- Multipart upload recovery cannot be applied to files that are uploaded via multipart and also linked to a batch.
- Multipart upload is only available for asynchronous scans. Local scan, and synchronous scan are not supported.
- Multipart upload is not applicable for MetaDefender Core installed in non-persistence mode.

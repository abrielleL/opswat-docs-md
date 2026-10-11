<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/add-a-google-cloud-storage -->

# Add a Google Cloud Storage

In order to integrate Google Cloud with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Inventory**, click on **Add account** and choose **Google Cloud**

![](https://uploads.developerhub.io/prod/k8zL/5b6acr6wixvgr3mdftzfndhy68gpcf23r2qavurrhx2gwjbigjo7ojkeoahu6r1r.png)

2. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later
3. There are two ways to connect:

- **via the ADC from the ECS instance** (If you choose this option, skip the following step and continue from step 5)
- **using security credentials**

4. Upload your **Credentials** file. Scroll down for more details.
5. Click Next in order to finish the process
6. Add an unit for the created account

![](https://uploads.developerhub.io/prod/k8zL/3flwpxssowpgwuwdg4xgcpcl7dccm0f008kfdle5a742dzh7m148romm3ey2uyjl.png)

7. Give your unit an unique name
8. Assign your unit to a Group
9. Enter the **name of the bucket** you wish to process with MetaDefender Storage Security.
10. If you wish to only process a particular folder enter the name or path of the folder in the **Folder location** field. Leave this field empty if you wish to process the entire bucket.
11. Select **Next** in order to finish the process.

> **Info**
>
> To be able to use **autodiscovery**, the credentials should have at minimum the **Storage Legacy Bucket Reader** (**roles/storage.legacyBucketReader**) role

### Where can I generate the Credentials file?

To generate a credentials file, please follow these steps, explained in the official documentation of Google Cloud.

[https://developers.google.com/workspace/guides/create-credentials#service-account](https://developers.google.com/workspace/guides/create-credentials#service-account)

### Using ADC for Google Cloud integration

On Google Cloud integration with ADC, the default credentials configured on the ECS instance will be used to authenticate.

Please use the following links to attach application default credentials to the ESC instance:

[https://cloud.google.com/docs/authentication/application-default-credentials](https://cloud.google.com/docs/authentication/application-default-credentials)

[https://cloud.google.com/iam/docs/impersonating-service-accounts#attaching-to-resources](https://cloud.google.com/iam/docs/impersonating-service-accounts#attaching-to-resources)

> **Warning**
>
> If the google credentials are **not** set in the **GOOGLE_APPLICATION_CREDENTIALS** variable, then the service account assigned to the VM instance requires the **iam.serviceAccounts.signBlob** permission (included in the **Service Account Token Creator** role) and the `https://www.googleapis.com/auth/iam`  OAuth access scope (or the broader `https://www.googleapis.com/auth/cloud-platform`  scope).

### Using GCP Buckets With Hierarchical Namespace (HNS)

We recommend enabling **Hierarchical Namespace (HNS)** on your Google Cloud Storage buckets. When HNS is enabled, folder paths behave as true directories, allowing MetaDefender Storage Security to correctly validate and process **empty folders** and **folders containing only subfolders**.

**With HNS enabled:**

- Empty folders can be added as destinations
- Folder existence is reliably detected

**Without HNS:**

- Empty folders may be rejected as “non-existent”
- Hidden system objects may affect folder validation

Learn more in Google’s official documentation: [https://docs.cloud.google.com/storage/docs/folders-overview](https://docs.cloud.google.com/storage/docs/folders-overview)

### Google Cloud: Handling Rate Limiting

For transient errors on Google Cloud requests a retry with exponential backoff can be configured to adjust the required needs. The HTTP error codes covered are the `TooManyRequests`, `RequestTimeout`and `ServiceUnavailable`.

The retry policy can be customized using the following environment variables:

| Parameters | Value |
| ---- | ---- |
| GCP_MAX_RETRY_ATTEMPTS | 10 |
| GCP_MAX RETRY_DELAY | 120 (seconds) |

The retry policy implements exponential backoff, starting with a 200-millisecond delay between retries and capping at a maximum delay of 120 seconds after 10 retries.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

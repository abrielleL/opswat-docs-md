<!-- source: https://www.opswat.com/docs/mdss/integrations/add-an-alibaba-cloud-storage -->

# Add an Alibaba Cloud Storage

In order to integrate Alibaba Cloud with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose **Alibaba Cloud** and click **Next**
2. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later
3. Enter the **Endpoint** URL for *Access Over Internet*. Scroll to the end of this page for more details.
4. There are two ways to connect:
   - **via the RAM role from the ECS instance**: select **Use RAM Role** (If you choose this option, skip the following two steps and continue from step 7)
   - **using security credentials**
5. Enter your **Access Key ID**. Scroll to the end of this page for more details.
6. Enter your **Access Key Secret .** Scroll to the end of this page for more details.
7. Click **Next** to create the account
8. On the **Summary** step, click **Add unit** (or navigate to **Inventory**, click **Add New** > **Unit**, choose the previously created account and click **Next**)
9. Give your unit a name so you can easily identify it later
10. Assign your unit to a Group
11. Enter the **name of the bucket** you wish to process with MetaDefender Storage Security.
12. If you wish to only process a particular folder enter the name or path of the folder in the **Folder location** field. Leave this field empty if you wish to process the entire bucket.
13. Select **Next** in order to finish the process.

### Where can I find the Endpoint URL?

The endpoint URL can be found in the following list of the official documentation of Alibaba Cloud.

[https://www.alibabacloud.com/help/en/object-storage-service/latest/regions-and-endpoints](https://www.alibabacloud.com/help/en/object-storage-service/latest/regions-and-endpoints)

### Where can I find the Access Key ID and Access Key Secret?

To generate an Access Key ID / Access Key Secret  pair please follow these steps, explained in the official documentation of Alibaba Cloud.

[https://www.alibabacloud.com/help/en/basics-for-beginners/latest/obtain-an-accesskey-pair](https://www.alibabacloud.com/help/en/acr/create-and-obtain-an-accesskey-pair)

### Using RAM role for Alibaba Cloud integration

On Alibaba Cloud integration with RAM, the role configured on the ECS instance will be used to authenticate.

Please use the following links to configure and attach a RAM role to the ESC instance:

[https://www.alibabacloud.com/help/en/ram/product-overview/best-practices-for-identity-and-access-control](https://www.alibabacloud.com/help/en/ram/product-overview/best-practices-for-identity-and-access-control)

[https://www.alibabacloud.com/help/en/elastic-compute-service/latest/use-ram-roles-to-access-other-alibaba-cloud-services](https://www.alibabacloud.com/help/en/elastic-compute-service/latest/use-ram-roles-to-access-other-alibaba-cloud-services)

[https://www.alibabacloud.com/help/en/elastic-compute-service/latest/attach-an-instance-ram-role](https://www.alibabacloud.com/help/en/elastic-compute-service/latest/attach-an-instance-ram-role)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

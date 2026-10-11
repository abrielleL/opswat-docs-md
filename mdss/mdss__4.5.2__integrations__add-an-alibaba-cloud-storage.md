<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/add-an-alibaba-cloud-storage -->

# Add an Alibaba Cloud Storage

In order to integrate Alibaba Cloud with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Storage units**, click on **Add storage unit** and choose **Alibaba Cloud**

![](https://uploads.developerhub.io/prod/k8zL/op0y467uqagu758yy31vzby6x3y3urv18xihfa30n1l0eoi0ci9vibi4uq370o0c.png)

2. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later
3. Give your storage a name so you can easily identify it later
4. Enter the **Endpoint** URL for *Access Over Internet*. Scroll to the end of this page for more details.
5. There are two ways to connect:
   - **via the RAM role from the ECS instance** (If you choose this option, skip the following two steps and continue from step 7)
   - **using security credentials**
6. Enter your **Access Key ID**. Scroll to the end of this page for more details.
7. Enter your **Access Key Secret .** Scroll to the end of this page for more details.
8. Enter the **name of the bucket** you wish to process with MetaDefender Storage Security.
9. If you wish to only process a particular folder enter the name or path of the folder in the **Folder location** field. Leave this field empty if you wish to process the entire bucket.
10. Select **Continue** in order to finish the process.

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

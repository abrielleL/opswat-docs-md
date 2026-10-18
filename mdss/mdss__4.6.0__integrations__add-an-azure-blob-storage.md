<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/add-an-azure-blob-storage -->

# Add an Azure Blob Storage

In order to integrate Azure Blob with MetaDefender Storage Security you will be required to create an application registration, assign the necessary permissions and roles, and then generate a secret key. Please follow these steps:

1. From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose **Azure Blob** and click **Next**

![](https://uploads.developerhub.io/prod/k8zL/3je4codf7uq9b572rnyqegv0clccqeu77e9rso1uhsmonbn25iytnax6zodnfmex.png)

2. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later
3. Enter the Azure **Storage Account** name.
4. Select **Government Cloud type** if the storage belongs to Azure US Government Cloud.
5. Enter your **Tenant ID**. Scroll to the end of this page for more details.
6. Enter your **Client ID.** Scroll to the end of this page for more details.
7. Enter your **Client Secret.** Scroll to the end of this page for more details.
8. Click Next to finish the process.
9. Add a new unit for the created account

![](https://uploads.developerhub.io/prod/k8zL/0yjxtj1od1xxhqn9yxz3x1q24l24vqe6sxrgot77tmo9mvd0up95vwzygwivuldc.png)

10. Enter an unique name for your unit.
11. Assing your unit to a Group
12. Enter the **name of a container** to process objects from a particular container.
13. Select **Next** in order to finish the process.

### How to create an Azure Blob application?

In order to process your Azure Blob objects with MetaDefender Storage Security you will be required to add a new app registration in your Microsoft Entra ID Azure Portal.

1. Log in to [Azure Portal](https://portal.azure.com/) and from the left navigation menu choose **Microsoft Entra ID**

![](https://uploads.developerhub.io/prod/k8zL/zukcu961w7ji11ybtdre9lxqxyezk1617fd67mxq1f134tpa800uksj61tq9tvak.png)

2. Make a copy of the **Tenant ID** from the overview page

![](https://uploads.developerhub.io/prod/k8zL/s4ar7lb5al3lqakx4tsvbhp5rrv1lsgv4ajcl5lqd095luysk82xbbpd4xxo6fn6.png)

3. From the left side menu, choose **App registrations**
4. Click **New registration**
5. Give your app a name so you can easily identify it

![](https://uploads.developerhub.io/prod/k8zL/k0fegz2y5aom4xs0iz2pdz704urx4bu5jaemumv3w35fzfq7c7njxnih7u3bofp5.png)

6. There is no need to modify the other properties. When ready, please click **Register**
7. From the **Overview** page of your newly created application, make a copy of **Application (client) ID**
8. Navigate to **Certificates & Secrets** from the left-side menu
9. Click **New client secret** and choose Expires in 24 months

![](https://uploads.developerhub.io/prod/k8zL/bdz3ch0y68si6prb4apvuouhc6eqhauqd9ko8xnjyh558l99xrah3goq65scdsng.png)

10. Click Add and then you will need to make a copy of the generated secret key because it will not be available later
11. Navigate to your **Storage Account** and select the **Access Control (IAM)** menu
12. Select the **Role assignments** tab, then select the **Add role assignment** option from the **Add** dropdown.

![](https://uploads.developerhub.io/prod/k8zL/jgigpz4cmuj0asaruc3mw94h02h048d327y7dlmev323rxma13ruo68zcto89t9q.png)

13. Assign the following roles to the **Client Application** you previously registered:
    1. Storage Blob Data Contributor
    2. Reader
14. Navigate back to your **Storage Account** and from **Security + networking** menu, select **Networking**

![](https://uploads.developerhub.io/prod/k8zL/er4pyfb671l7tdpcgmdkxphrdzws53a443ubgfq3lptj855cklhn6xmwhedbjdoa.png)

15. Navigate to **Public access** tab (the first and default one)

![](https://uploads.developerhub.io/prod/k8zL/ts9ckidkhjvdlroe8qtrof4wvbhfpfa8ca45qyyauc4llggxxheyrhunsoibd454.png)

16. Click Manage on the Public network access section

![](https://uploads.developerhub.io/prod/k8zL/h4q7l66h2y4moag0eytpoja19y6fnlj9jlo2kmxzbjwyhd4fbj2fvxhqsbi0u58l.png)

17. Enable **Public network access**

![](https://uploads.developerhub.io/prod/k8zL/4fummok2wcdlt6t656z7xqunsm12vbomga3ebholnfivi53hwjenpflnsyif79ew.png)

18. From the **Public network access scope**, you have two options:
    1. Enable from all networks: this is less restrictive and will allow any applications to try to establish a successful connection to your storage account.
    2. Enable from selected networks: this will restrict access only to specific IPv4 addresses. If you enable this option, add the public IP address from which MetaDefender Storage Security reaches Azure. For a Docker or Windows deployment this is the public address the host machine uses for outbound traffic: its own IP, or the address of the NAT or firewall in front of it. For a Kubernetes deployment it is the public address the cluster uses for outbound traffic, such as a NAT gateway or load balancer; if the nodes reach the internet through their own public IPs, add the address of every node that runs MDSS services. The Storages, Discovery, Remediations and Scanning services all connect to the storage account from that address, including when a file is moved from Azure Blob to another type of storage unit.

![](https://uploads.developerhub.io/prod/k8zL/3rmna0tz6wvmxhlsx9v57gmcm0ps4n0v00myhol3clhp67itexfk1bhb1jwnqcyf.png)

19. Now that you have the **Tenant ID**, **Client ID** and the **Client Secret Key**, you can go back in **MetaDefender Storage Security** and finish the Azure Blob integration. Congratulations!

For additional configuration of how MetaDefender Storage Security handles blobs please check [custom configuration](https://www.opswat.com/docs/mdss/configuration/custom-configuration).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

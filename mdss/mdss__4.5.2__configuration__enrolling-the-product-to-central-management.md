<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/enrolling-the-product-to-central-management -->

# Enrolling the product to Central Management

To enroll MetaDefender Storage Security into My OPSWAT Central Management, these steps should be followed:

1. In the top-right corner, next to the username, there will be a button with the text **Unmanaged** (if the product is not yet enrolled to Central Mangement; if the product is already enrolled, the text will say **Managed**)

![](https://uploads.developerhub.io/prod/k8zL/58mgvrqcka8o9xc0w6wxk5ui2zoxldjoytluyicif9u9ainai6vx1qr8wcxcxmpz.png)

2. Clicking the button will open a form containing the necessary fields to enroll. These are **Server URL**, which is the address of the Central Management server to which you want to enroll the product, and **Registration Code**, which can be found in the Central Management UI by navigating to **Settings -> Global**. The registration code will be present on that page.

![](https://uploads.developerhub.io/prod/k8zL/okx5ypmqma1vv5178axna9p9vtmuv7dz8x6e40oe0c571vbni1upafwlnh6607z6.png)

3. Additionalliy, you can provide a **Custom IP**. This constitutes the **IP** of the MDSS instance, not the Central Management one.

![](https://uploads.developerhub.io/prod/k8zL/2vw08neu8i55rz6nr944z3nxdvolsmgh6m2m7gvggs6lveb86rb72svkb2uhdp7x.png)

4. After completing the form, click on **Enroll Now.** If the information is correct, MDSS should display a message saying that enrollment was successful.

Once you have successfully enrolled your MetaDefender Storage Security instance, the button will now have the text **Managed** and clicking on it will reveal additional information about the connection to the Central Management platform.

![](https://uploads.developerhub.io/prod/k8zL/fqt4ll9oabx46xhn16r0psgfarqmiqpjf1eoxeto71isjrjtkgz7e8svttskku7x.png)

Additionally, navigating to the Central Management server, you should be able to see your enrolled instances under the **Products** tab

![](https://uploads.developerhub.io/prod/k8zL/l8iutssdgpvtnndbymy2gxcxjzgoq70h2fe0hr2f35uetda6gbzc2u22aum5vtl9.png)

Furthermore, clicking on the card above will take you to a page where more information about each instance can be seen

![](https://uploads.developerhub.io/prod/k8zL/g5fhgxihb4ndbpdazjk5fzlbhvy8fmqvrvpgken0vrz9y2eexf5xodnobnt4zozz.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

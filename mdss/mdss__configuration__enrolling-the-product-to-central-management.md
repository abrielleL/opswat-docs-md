<!-- source: https://www.opswat.com/docs/mdss/configuration/enrolling-the-product-to-central-management -->

# Enrolling the product to Central Management

To enroll MetaDefender Storage Security into My OPSWAT Central Management, these steps should be followed:

1. In the top-right corner, next to the username, there will be a button with the text **Unmanaged** (if the product is not yet enrolled to Central Mangement; if the product is already enrolled, the text will say **Managed**)

2. Clicking the button will open a form containing the necessary fields to enroll. These are **Server URL**, which is the address of the Central Management server to which you want to enroll the product, and **Registration Code**, which can be found in the Central Management UI by navigating to **Settings -> Global**. The registration code will be present on that page.

3. Additionalliy, you can provide a **Custom IP**. This constitutes the **IP** of the MDSS instance, not the Central Management one.

4. After completing the form, click on **Enroll Now.** If the information is correct, MDSS should display a message saying that enrollment was successful.

Once you have successfully enrolled your MetaDefender Storage Security instance, the button will now have the text **Managed** and clicking on it will reveal additional information about the connection to the Central Management platform.

Additionally, navigating to the Central Management server, you should be able to see your enrolled instances under the **Products** tab

Furthermore, clicking on the card above will take you to a page where more information about each instance can be seen

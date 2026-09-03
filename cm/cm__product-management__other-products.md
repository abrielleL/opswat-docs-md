<!-- source: https://www.opswat.com/docs/cm/product-management/other-products -->

# Enroll other Products

To enroll other OPSWAT on-premises products' instances to My OPSWAT Central Management, you need the information below.

- a registration code from your account that can be found in the **Account** tab of the **Settings** page.
- server API URL that you can obtain from My OPSWAT Central Management

Here are steps to find these information

- Log into My OPSWAT Central Management
- Click **+Enroll Product** button on the left navigation
- Click a product name button
- A registration code and server URL will be shown on the enrollment dialog

![](https://uploads.developerhub.io/prod/97qW/g9zxawbdqmr5vy9xffevd1rfee4nstj6dkkyf5z638eokbzkl1bs30i345ugcvwq.png)

### [Steps to enroll a product instance to My OPSWAT](https://www.opswat.com/docs/product-management/configuration/enroll-instances#steps-to-enroll-a-product-instance-to-my-opswat) Central Management

You can either enroll a product instance during a product Setup wizard OR after you log into the product console UI.

Log into the product instance's console to enroll it to your account with My OPSWAT Central Management. The product instance needs Internet connection or at least a connection to the above Server API URL at port 443.

#### On the Product Console UI

On a product console UI, you can follow the below steps to enroll an instance to My OPSWAT central management after logging into the console as an administrator user.

- click Unmanaged on the top right if the instance has not managed by My OPSWAT central Management
- An enrollment dialog will be shown up. Enter the below information and then click Enroll Now
  - Server API URL
  - Registration code
- If the product can enroll itself to My OPSWAT Central Management, the instance's state is now managed and you can check its connection status to My OPSWAT Central Management by clicking Managed on the top right

#### From the Setup wizard

A product's setup wizard may offer you a step to enroll the product instance to My OPSWAT Central Management. Simply enter a registration code on your account and server API URL and click Enroll button.

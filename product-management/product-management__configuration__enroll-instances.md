<!-- source: https://www.opswat.com/docs/product-management/configuration/enroll-instances -->

# Enroll Instances

To enroll your OPSWAT on-premises products' instances to My OPSWAT, you need the information below.

- a registration code from your account that can be found in the **Organization** tab of the **Settings** page.
- server API URL:

  - My OPSWAT Cloud: <https://product.my.opswat.com>
  - My OPSWAT On-premises: [http|https]://<your My OPSWAT server address>. For example: <http://myopswat.yourcompanydomain.com>

Log into the product instance's console to enroll it to your account with My OPSWAT. The product instance needs Internet connection or at least a connection to the above Server API URL at port 443.

### [Registration Code](/docs/product-management/configuration/enroll-instances#registration-code)

You can find the registration code in the **Organization** tab of the **Central Management** > **Settings** page, which can be found on the left navigation menu.

### [Steps to enroll a product instance to My OPSWAT](/docs/product-management/configuration/enroll-instances#steps-to-enroll-a-product-instance-to-my-opswat)

Disclaimer

Screenshots in this section were taken from MetaDefender Core v5.6.1. If you enroll with other products, the user interface (UI) may be a bit different

You can either enroll a product instance during a product Setup wizard OR after you log into the product console UI.

#### [On the Product Console UI](/docs/product-management/configuration/enroll-instances#on-the-product-console-ui)

On a product console UI, you can follow the below steps to enroll an instance to My OPSWAT after logging into the console as an administrator user.

- click Unmanaged on the top right if the instance has not managed by My OPSWAT or [OPSWAT Central Management](https://docs.opswat.com/ocm)

- An enrollment dialog will be shown up. Enter the below information and then click Enroll Now

  - Server API URL as <https://product.my.opswat.com>
  - Registration code: your registration that can be found in Settings > Account tab on My OPSWAT

- If the product can enroll itself to My OPSWAT, the instance's state is now managed and you can check its connection status to My OPSWAT by clicking Managed on the top right

#### [From the Setup wizard](/docs/product-management/configuration/enroll-instances#from-the-setup-wizard)

A product's setup wizard may offer you a step to enroll the product instance to My OPSWAT. Simply enter a registration code on your account and server API URL as <https://product.my.opswat.com> and click Enroll button.

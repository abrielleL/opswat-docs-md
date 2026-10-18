<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/azure-specific-configuration -->

# Azure AD Specific Configuration

To set up Azure AD SSO for MDSS, follow these steps:

1. In the Microsoft Azure portal, navigate to **App registrations** and click on **New registration**

![](https://uploads.developerhub.io/prod/k8zL/zj0t0fngzsiqcqxw42pyjnxqhpv4d2riymtj30bwcpciouqu6bxn8blc1ot9elch.png)

2. In the **Register an application** window, enter a name for your application, select your preferred configuration for **Supported account types** (recommended is Single tenant), and configure the **Redirect URI**. The redirect URI should be composed of the address where MDSS is deployed, along with the **/callback** suffix added to the path.

![](https://uploads.developerhub.io/prod/k8zL/4a3dketpugd8vlvmdvekjq76mhfh7m0a5q2501jzdts5c6e3z8jln129p5emlolp.png)

3. Afterwards, navigate to the **Overview** tab. There, to successfully configure the SSO Configuration in MDSS afterwards, store the **Application (Client) ID** and the **Direcory (Tenant) ID** somewhere safe on your computer. Then, click on the **Endpoints** button.

![](https://uploads.developerhub.io/prod/k8zL/c1w2bi0dpchzqn9c26wr9exbe3kqtp7jvdn4grirss8povs9m7x88sw5ccn9bemw.png)

4. There, the authority URL is located in the right-hand side menu and is the following: **"https: //login.microsoftonline.com/<YOUR-TENANT-ID >/v2.0"**

![](https://uploads.developerhub.io/prod/k8zL/djqjwqzb8dcgv7s19fqofz98qsygf210jvl1gvjm9c0qvw07gjxyfupn8g02gbvo.png)

5. Navigate to the **Certificates & secrets** tab and click on **New client secret**

![](https://uploads.developerhub.io/prod/k8zL/w7xml0d8hiq0b51lfws5bmc3kokebh7zahbb6hqzt2896enctbsfryk5ff3bz618.png)

6. Give a description to your client secret, configure the expiration to your liking, and add it

![](https://uploads.developerhub.io/prod/k8zL/45ualwm1p561xuh7y22js9vx1gma48v4nc118bwtdxx1u9ug7lwehoy7acy03skp.png)

7. Copy your secret value and store it somewhere safe on your computer (you will only be able to copy it at this stage)

![](https://uploads.developerhub.io/prod/k8zL/9ipa5bysbgz5z6gawyedo9gtgwi7lvquti2tktpqc7qr8lrrvlks712s6qgb9n6g.png)

8. Navigate to **App Roles** and click on **Create app role**

![](https://uploads.developerhub.io/prod/k8zL/mzxz7nn85uxms7mnjkf77i7ui4okverljp2tcphek2dycrqnxfv0dtv3l7k8ray1.png)

9. Give your role a Display name, configure the **Allowed member types** to be set to **Both (Users/Groups + Applications)**. Then, for the value, give one of the two values to determine the role that this user will have within MDSS:

- **SsoAdministrator** - equivalent to the administrator role in MDSS
- **SsoReadOnlyAdministrator** - equivalent to the read-only admin role in MDSS

![](https://uploads.developerhub.io/prod/k8zL/xd6cqc9lky5jyj7hdsosqeriz9vf911p7q3gwd6jp6wejlupy4kfm5c6rejbbxzn.png)

10. Navigate to the **API permissions** and click on **Add a permission**. Then, select the **My APIs** tab and find your app

![](https://uploads.developerhub.io/prod/k8zL/vznwi89a4psuz8mhqpi07arum6oa7f7p984yi8nmbu325myilk7d5euutwxo01di.png)

11. Click on your app and select the app role you have configured.

![](https://uploads.developerhub.io/prod/k8zL/5we8ohk6760as0kj95k86goc05rhnjy85y1b7if2oxes4p001d3tebnt2ayzospz.png)

12. Next, click on **Grant admin consent**

![](https://uploads.developerhub.io/prod/k8zL/fn3zkgknnfkvb61cfq6t64sxa0pud8dm2q8ya7rg74tv1l3mm4goqjsgj85u7zb3.png)

13. Go to the **Authentication** tab. Here, click **Add a platform** and select the **Web** option. Then, click on the checkbox for **ID tokens** and also for **Supported account types**, select whatever you prefer (recommended is Single tenant).

![](https://uploads.developerhub.io/prod/k8zL/bimguoy8zfk4uyk2zpxha1lcgtcoz713tg083htp6jqn1fybyk2vqdyu25kxtlr2.png)

![](https://uploads.developerhub.io/prod/k8zL/4615z9hhclodfeh82teg0lsk532uyhzvgcb8un0pzrz80jglbvu1g2skd13rv3zb.png)

14. Now, leave the **Azure Portal** and navigate to the **Microsoft Entra admin center**. Here, find the **Enterprise applications** window under the **Applications** tab on the left. Search for your configured app.

![](https://uploads.developerhub.io/prod/k8zL/90z5vfi2ae9rfm7vvwe1qus3q0yqvli9bpnlck034vr30gvf98ge4xnq1i9blqz7.png)

15. Navigate to the **Users and groups** tab and select  **Add user/group**

![](https://uploads.developerhub.io/prod/k8zL/djv0fiztr9gzlzfwc1s0e4nlwonhqvs6jvf9r098m86ij2fmbu53b4qppjpu1qpq.png)

16. Find your user and assign the configured App Role to it.

![](https://uploads.developerhub.io/prod/k8zL/jzt31uopnvkt7bcwq8o487wr8yae05jsaup6vf88ehnhcny225xuofc4jpyhlq11.png)

17. Lastly, navigate to **App registrations**, find your app and click on the **Token configuration**. There, click on **Add optional claim**, select **ID**, and add the **email** claim.

![](https://uploads.developerhub.io/prod/k8zL/51frzk7cglqnoya74zlvtkba819w0wdouy1oef7bvpv8nydd66cqal97vizrms89.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

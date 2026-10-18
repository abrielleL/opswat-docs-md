<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/okta-specific-configurationv3o -->

# Okta Specific Configuration

> **Info**
>
> To properly access MDSS, the following Okta **Groups** are required
>
> **Solution:**
>
> Create a Perquisite section on providing specific instructions on how to add the Specific Group and and assign users to them.
>
> For Example:
>
> **Prerequisite:**
>
> The following specific groups needs to be added into OKTA:
>
> **SsoAdministrator** - the equivalent of local MetaDefender Storage Security administrator role.
>
> **SsoReadOnlyAdministrator** - the equivalent of local MetaDefender Storage Security read-only role.
>
> To add the two required groups in Okta, navigate to **Directory > Groups**, then select **Add Group**.
>
> ![](https://uploads.developerhub.io/prod/k8zL/5k9qjm44af8peaz3yxv4nyamohwv0kh93s3tkylghgsexgfq13vjepevjdz4divy.png)
>
> Within the specific group, ensure that users are assigned by selecting the **Assign People** option.
>
> ![](https://uploads.developerhub.io/prod/k8zL/zjmemv4jjklg6yi2v6cwf7lumjdkxsw1ciyekadd4xnxkvbya1z8s8fb61gizt9w.png)
>
> This will help ensure that Okta administrators remember to create the necessary groups and properly assign users to them.

To set up Okta SSO for MDSS, follow these steps:

1. Under the **Security** tab, go to the **API** section, locate your **Authorization Server** and click on the pencil icon to edit

![](https://uploads.developerhub.io/prod/k8zL/bwt18e8imv5uv2lixnb7zjadsabs896li7otpwolcqw91ngxm5j1qfhs8sannu3z.png)

> **Info**
>
> The **Issuer URI** from the **Authorization Server** should be inputted as the **Authority URL** of the MDSS SSO Configuration.

2. Within the **Scopes** tab, add a new scope. Name it "***groups***", select **Implicit** for the **User Consent**, and check the **Include** in public metadata checkbox

![](https://uploads.developerhub.io/prod/k8zL/of0exvhatw3u8qtfdf9c3b0sdipqyaab9qitrzahqunrugvaqbhxs5wdaet4lxr1.png)

3. Within the **Claims** tab, add a new claim. Name it "***groups***", select **Id Token** and **Always** from the **Include** **in token type** dropdowns, select **Groups** as the **Value Type**, input "**.***" next to **Matches regex** to get all groups, and include it in the previously created "***groups***" scope

![](https://uploads.developerhub.io/prod/k8zL/0z2aqoa3fwgf3v6edhviu8rhojfihsd59mqe07wlvvbq24cwinlg7062o60mrh1g.png)

4. Navigate to the **Applications** tab and select the **Applications** section. Afterwards, click "**Create App Integration**"

![](https://uploads.developerhub.io/prod/k8zL/8hcwtj49c47ncuu3csuqo0znoworcb2h1o14lktbczepij576ws9ckbqflv9lvhz.png)

5. For the **Sign-in method**, select **OIDC - OpenID Connect**, and for the **Application Type**, select **Web Application**

![](https://uploads.developerhub.io/prod/k8zL/avwhsib4qcczv0qw62kxo32bk68s4sds7jwm33aw7ocq7i3y84k8hxwbbin4ar2l.png)

6. Give your app integration a name, for the **Grant Type,** tick the checkboxes. Under the **Sign-in redirect URIs**, write the the base URL of the MDSS deployment, followed by the "**/callback**" suffix. For the **Controlled access**, select **Allow everyone in your organization to access.**

![](https://uploads.developerhub.io/prod/k8zL/ywnh6yr4ubck6n4rm7fjoqho2hllo5zybazatwt7yc819qi6jx66459t4t0uacaa.png)

7. Save the **Client ID**, select **Client Secret** for the Client authentication, generate a new secret and save it.

![](https://uploads.developerhub.io/prod/k8zL/04h2g5xo3zha30otmk084b73vsjpbqdgz6y1lfgrngv1nr52p32221j442b4tje5.png)

8. Within your **Application**, navigate to the **Sign On** tab, and scroll down to **OpenID Connect ID Token**. There, click the edit button and, for the **Groups Claim Type**, select **Filter**, and for the **Groups Claim Filter**, select **groups**. Select **Matches regex** from the dropdown and input "**.***"

![](https://uploads.developerhub.io/prod/k8zL/pnfk1p0wtoj5szhoad08fosf6tadetvy12uvo22oh3ir7xuo12khnp841ec9u7up.png)

9. Under the **Security** tab, go to the **API** section, locate **Access Policies** and add a new one.

![](https://uploads.developerhub.io/prod/k8zL/wik99zsaom99e3r45holmyn74v1ig8i44a6uvdagyiw8jkc1hx9glqw7frndlvda.png)

10. Add policy and assign to **All clients** or **your desired clients.**

![](https://uploads.developerhub.io/prod/k8zL/gkle4f716wa3xir2dgx3y2nyq27kov3x4tbyt06hrldnlh59e7bdvsfxlsmt4o5i.png)

11. Create a rule, and make sure that on **Advanced** label you have checked **Implicit(hybrid).**

![](https://uploads.developerhub.io/prod/k8zL/pmot7y5571a9ingmyzf6qbnyu3pm1tl6zohzgihqe8yq9g5phcjglrictdzshxxv.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

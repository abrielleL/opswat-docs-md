<!-- source: https://www.opswat.com/docs/mdss/configuration/okta-specific-configurationv3o -->

# Okta Specific Configuration

To properly access MDSS, the following Okta **Groups** are required

**Solution:**

Create a Perquisite section on providing specific instructions on how to add the Specific Group and and assign users to them.

For Example:

**Prerequisite:**

The following specific groups needs to be added into OKTA:

**SsoAdministrator** - the equivalent of local MetaDefender Storage Security administrator role.

**SsoReadOnlyAdministrator** - the equivalent of local MetaDefender Storage Security read-only role.

To add the two required groups in Okta, navigate to **Directory > Groups**, then select **Add Group**.

Within the specific group, ensure that users are assigned by selecting the **Assign People** option.

This will help ensure that Okta administrators remember to create the necessary groups and properly assign users to them.

To set up Okta SSO for MDSS, follow these steps:

1. Under the **Security** tab, go to the **API** section, locate your **Authorization Server** and click on the pencil icon to edit

Info

The **Issuer URI** from the **Authorization Server** should be inputted as the **Authority URL** of the MDSS SSO Configuration.

2. Within the **Scopes** tab, add a new scope. Name it "***groups***", select **Implicit** for the **User Consent**, and check the **Include** in public metadata checkbox

3. Within the **Claims** tab, add a new claim. Name it "***groups***", select **Id Token** and **Always** from the **Include** **in token type** dropdowns, select **Groups** as the **Value Type**, input "**.***" next to **Matches regex** to get all groups, and include it in the previously created "***groups***" scope

4. Navigate to the **Applications** tab and select the **Applications** section. Afterwards, click "**Create App Integration**"

5. For the **Sign-in method**, select **OIDC - OpenID Connect**, and for the **Application Type**, select **Web Application**

6. Give your app integration a name, for the **Grant Type,** tick the checkboxes. Under the **Sign-in redirect URIs**, write the the base URL of the MDSS deployment, followed by the "**/callback**" suffix. For the **Controlled access**, select **Allow everyone in your organization to access.**

7. Save the **Client ID**, select **Client Secret** for the Client authentication, generate a new secret and save it.

8. Within your **Application**, navigate to the **Sign On** tab, and scroll down to **OpenID Connect ID Token**. There, click the edit button and, for the **Groups Claim Type**, select **Filter**, and for the **Groups Claim Filter**, select **groups**. Select **Matches regex** from the dropdown and input "**.***"

9. Under the **Security** tab, go to the **API** section, locate **Access Policies** and add a new one.

10. Add policy and assign to **All clients** or **your desired clients.**

11. Create a rule, and make sure that on **Advanced** label you have checked **Implicit(hybrid).**

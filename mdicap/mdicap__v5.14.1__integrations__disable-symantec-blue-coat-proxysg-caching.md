<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/disable-symantec-blue-coat-proxysg-caching -->

# Disable Symantec Blue Coat ProxySG caching

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Step-by-step guide](/docs/mdicap/v5.14.1/integrations/disable-symantec-blue-coat-proxysg-caching#step-by-step-guide)

To prevent the transmission of stale content or other issues caused by object caching, you can use either cache(no) or bypass_cache(yes) in content policy language (CPL). For a comparison of cache(no) and bypass_cache(yes), see [KB1772](http://kb.bluecoat.com/index?page=content&id=KB1772).

This sample provides instructions for disabling object caching for specific URLs by adding a policy rule in the Web Access Layer.

1. In the Management Console, select **Configuration** > **Policy** > **Visual Policy Manger**, and then click **Launch**.
2. From the Visual Policy Manager (VPM) dialog box, select **Policy > Add Web Access Layer**. The Add New Layer dialog box appears.
3. In the Add New Layer dialog box, name the layer to reflect the purpose of the layer, such as "Web Access Layer (bypass cache)," then click **OK**.
4. Right click the **Destination** field and select **Set** from the drop-down list.
5. In the Set Destination Object dialog box, click **New > Request URL,** and enter the URL you want to exclude from the cache. Click **Add,** then **OK**.
6. Right click on **Action** and select **Set** > **Bypass Cache.** Then, click **OK**.
7. Click **Install policy** to apply the new policy.

To use CPL code for the same policy rules, add the following CPL code in the local policy file or in a VPM CPL Policy Layer:

<Proxy> url.domain=<*url*> bypass_cache(yes)

In the example above, <*url*> is the URL you want to exclude from caching.

Info

Source:

<https://support.symantec.com/us/en/article.tech241976.html>

## [Related Information](/docs/mdicap/v5.14.1/integrations/disable-symantec-blue-coat-proxysg-caching#related-information)

Error rendering macro 'contentbylabel' : parameters should not be empty

<!-- source: https://www.opswat.com/docs/supply-chain/configuration/configuring-an-api-key -->

# Configuring an API Key

For security purposes, an API Key, once displayed, cannot be retrieved again. Store your API Key securely, as it will be required each time you configure webhook registration. This API Key serves as the secret key for HTTP POST header authentication.

### Steps to Generate an API Key:

1. Navigate to **Users**.
2. Locate your user name, click the three-dot (ellipsis) options menu, and select **Configure API Key**.

![](https://uploads.developerhub.io/prod/jdK6/2m1amuh7cd8m33ux4qqru11zji8m7i9plscx28m8uudf7osqxy3xjvba79u71qny.png)

A popup window will appear:

![](https://uploads.developerhub.io/prod/jdK6/yo8bmpkscfxizhxdhxd7knmfjpu57c343karqn9zp3x3yn85lq1nn9irh2gui3eu.png)

3. Click on **Generate New** to create a new API Key.

- A new API Key will appear. Note: This key is inactive until the next step is completed.
- Ensure you securely copy this key immediately, as it will not be visible again once saved.

![](https://uploads.developerhub.io/prod/jdK6/v58tj183vmw4oje5sv5v6u4swixcsft6q4ntg8cliaifoyarayurj349m3kamuzs.png)

4. Click **Save and Copy** to activate the new API Key and replace any existing key.

> **Update the places that use the old key**
>
> Each user has one API key. When you save a new key, the old key stops working. Update the new key in these places:
>
> - **Webhooks:** the webhook secret or the `ApiKey` header in your service providers. A webhook uses the API key of the user who created the webhook URL.
> - **Cross Domain Transfer:** the **Authorization Token** in the Low Side setup, if the key belongs to a High Side user.
>
> Events and transfers fail until you update the key.

## Use the API Key in a request

Include your API key in the HTTP request headers using the `ApiKey` header.

```bash
curl -X POST "https://YOUR_ENDPOINT_URL" \
  -H "Content-Type: application/json" \
  -H "ApiKey: YOUR_API_KEY" \
  -d '{}'
```

```javascript
await fetch("https://YOUR_ENDPOINT_URL", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "ApiKey": "YOUR_API_KEY"
  },
  body: JSON.stringify({})
});
```

> **Tip**
>
> Keep the API key secret. Do not include it in URLs or client-side code.

> **Note:** API requests are limited to 12,000 per minute per user.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)

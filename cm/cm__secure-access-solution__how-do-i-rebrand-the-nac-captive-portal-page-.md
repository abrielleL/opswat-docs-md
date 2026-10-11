<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/how-do-i-rebrand-the-nac-captive-portal-page- -->

# How do I rebrand the NAC captive portal page?

Guests who connect to a network protected by MetaDefender NAC may be redirected to a captive portal sign-in page hosted by My OPSWAT Central Management. By default, this page shows the OPSWAT logo and color scheme. You can replace the logo and colors with your own by creating a **rebranding package** and assigning it to the captive portal.

## What can be customized

| Element | Customizable |
| ---- | ---- |
| Logo at the top of the page | Yes |
| Page and sign-in card background colors | Yes |
| Text, button, link, and icon colors | Yes |
| Page text (for example, "Welcome to the network") | No |
| Page URL | No |

The branding applies to the whole guest flow: sign-in, guest self-registration, forgot/set password, and the success and error pages.

> **Rebranding packages are shared**
>
> The same rebranding packages are also used for the MetaDefender Endpoint remediation page of any device groups they are assigned to. Changes to a package that is already in use affect every place it is assigned. Create a dedicated package for the captive portal if you want to brand them differently.

## Step 1: Download the rebranding package template

1. Go to **Settings** > **Rebranding**.
2. Click **Add New Package**.
3. Enter a **Name** (and optionally a **Description**) for the package.
4. Under **Rebranding**, select **Customize a package**.
5. Click **English** next to *Download modern rebranding package for customization* to download the template `.zip` file.

![](https://uploads.developerhub.io/prod/97qW/llwyg1jqy4xhwxdknwq3ciememsgg9e97ghwn06f1i1xvx219io3ikdnv6838oe9.png)

Keep this page open. You will upload the customized package here in Step 3.

## Step 2: Customize the package

Extract the downloaded `.zip` file. Only the files below affect the captive portal. Leave all other files (`category_*.json`, `rule_*.json`, and the remaining keys in `generic.json`) unchanged.

### Logo

Replace `logo.png`, `light_logo.png`, and `dark_logo.png` with your own logo. Keep the same file names and format:

- **Format:** PNG (a transparent background is recommended)
- **Size:** 264 x 112 pixels

### Colors

Open `generic.json` and edit the `nac_*` keys inside the `colors` object. Each value must be a 6-digit hex color in the form `#RRGGBB`.

| Key | Controls | Default |
| ---- | ---- | ---- |
| `nac_guest_auth_background` | Page background | `#F4F4F5` |
| `nac_guest_auth_popup_background` | Sign-in card background | `#FFFFFF` |
| `nac_guest_auth_text_primary` | Main text color; also tints input field borders, placeholders, and dividers | `#1B273C` |
| `nac_button_primary_background` | Primary button (**Sign In**) background | `#3074FC` |
| `nac_button_primary_color` | Primary button text | `#FFFFFF` |
| `nac_button_secondary_color` | Secondary button (**Register a guest account**) text | `#1B273C` |
| `nac_link_text_color` | Links (for example, **Forgot password?**) | `#1D6BFC` |
| `nac_success_icon_color` | Success icon | `#008A00` |
| `nac_failed_icon_color` | Error icon | `#CB0704` |
| `nac_failed_background` | Error message background | `#FAE6E5` |
| `nac_trademark` | Footer trademark text | `#707682` |

For example:

```json
"colors": {
  ...
  "nac_button_primary_background": "#0B5394",
  "nac_button_primary_color": "#FFFFFF",
  "nac_guest_auth_background": "#EEF3F8",
  "nac_link_text_color": "#0B5394",
  ...
}
```

### Re-package

Compress the files back into a `.zip` file. The files must be at the root of the archive, not inside a folder.

## Step 3: Upload the package

1. Return to the **Add New Package** page from Step 1.
2. Confirm **Customize a package** is selected, click **Choose File**, and select your `.zip` file.
3. Click **Add**.

## Step 4: Assign the package to the captive portal

1. Go to **RADIUS NAC** > **Captive Portal** and open the **Guest Registration Setting** tab.
2. In **Assigned Rebranding Package**, select your package.
3. Click **Save**.

![](https://uploads.developerhub.io/prod/97qW/3pimtyh2hslp9abn6n8o387z00naje2vnlxmiduwfhoubfmy9vhz9w3yfp4lmjyt.png)

## Step 5: Verify

Connect a guest device to the network, or open the captive portal in a new private browser window, and confirm that your logo and colors appear. Branding is loaded when the portal page opens, so a page that is already open will not change until it is reloaded.

## Notes

- To return to OPSWAT branding, select **Default** in **Assigned Rebranding Package** (assuming the **Default** package has not itself been customized).
- If an assigned package is deleted, the captive portal automatically reverts to the default OPSWAT branding.
- If your logo or colors cannot be loaded, the portal falls back to the default OPSWAT branding. Guests can still sign in.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)

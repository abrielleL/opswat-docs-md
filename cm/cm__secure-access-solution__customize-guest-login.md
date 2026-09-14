<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/customize-guest-login -->

# Customize Guest login

You can download a default rebranding package from My OPSWAT Central Management console and start customizing the logo and text in the package. Please make sure you follow the instructions below while you create a new rebranding package. My OPSWAT Central Management will not show a detailed error if you do not follow the below guideline today.

- **Don't alternate filenames** in the default package
- **Don't alternate field names** in all JSON file
- All JSON files must be **saved in UTF-8** format
- **Don't delete variables and html**, for example My OPSWAT Central Management, in JSON files
- The zip file should contain both logo.png and all JSON file **in the root folder**.

The screenshots and tables below show you how to customize color and logo for each section on the remediation page.

![](https://uploads.developerhub.io/prod/97qW/lriedegb1x7p30mletqj3a46r3ujh8on7385l4qc03zsxowx1ymnjpicwiw8ycme.png)

![](https://uploads.developerhub.io/prod/97qW/xcxrvk7wmmto3g89uywp3br3ri59mdjvzbxqi7h9rk0ub71qaj0nxk1s0xds1iwy.png)

#### **Table 1: Logo Guideline**

Instructions to logo on the remediation on the Guest login page.

rebranding.zip

| Section | File | Description |
| ---- | ---- | ---- |
| 03 | Logo.png | Replace the logo.png file in the rebranding package with your organization logo. |

#### **Table 2: Color Guideline**

Define colors you would like to use on the Guest login page.

File: generic.json

| Section | Color Parameter | Description |
| ---- | ---- | ---- |
| 01 | `nac_guest_auth_background` | This is indicates the background color of the whole page |
| 02 | `nac_guest_auth_popup_background` | This is used for the background color of the Guest form |
| 04 | `nac_failed_background` | The background color of the alert popup |
| 05 | `nac_failed_icon_color` | The color of the Warning icon displays on the alert popup |
| 06 | `nac_guest_auth_text_primary` | Apply the color for the normal text on the page, does not include button text and text link |
| 07 | `nac_button_primary_color` | Color of the text on the button Sign In (Login page) and Register (Registration page) |
| 08 | `nac_link_text_color` | Color of text link |
| 09 | `nac_button_primary_background` | Background color of the button Sign In (Login page) and Register (Registration page) |
| 10 | `nac_button_secondary_color` | Color of the text and border on the Sign In with SSO button |
| 11 | `nac_trademark` | Color of the trademark text at the end of page |
| 12 | `nac_success_icon_color` | Color of the icon display after a User successfully Sign in |

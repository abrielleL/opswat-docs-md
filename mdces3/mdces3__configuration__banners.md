<!-- source: https://www.opswat.com/docs/mdces3/configuration/banners -->

# Banners

Summarize Page

The **Banner Templates** feature allows administrators to create and manage banner disclaimers appended to emails processed by policies. These banners can inform recipients about security actions such as sanitization, potential threats, or policy enforcement.

## [Template List](/docs/mdces3/configuration/banners#template-list)

The **Templates** section under **Settings** provides a list of all available banner templates. Banners are typically added to emails to indicate security actions taken by **MetaDefender Cloud Email Security ™**.

- **Search Bar**: Locate specific banner templates by name.
- **Template Columns**:

  - **Banner Name**: The name assigned to the banner template.
- **Template Buttons**:

  - **Clone**: Clone the selected template.
  - **Delete**: Delete the selected template.
- **Pagination Controls**: Users can navigate through multiple pages of templates.

## [Editing a Banner Template](/docs/mdces3/configuration/banners#editing-a-banner-template)

Clicking on a banner template from the list opens the **Template Details** page, where users can configure the banner content.

### [Template Settings](/docs/mdces3/configuration/banners#template-settings)

- **Banner Template Name**: The display name of the template.

### [Banner Content Customization](/docs/mdces3/configuration/banners#banner-content-customization)

- **HTML Tab**:

  - Provides a rich text editor for formatting banner content.
  - Users can insert fields, format text, and customize the layout.
  - Example banner message: `This email has been sanitized using OPSWAT Deep CDR™ technology. For more information, please visit https:///www.opswat.com`
- **Plain Text Tab**:

  - Used for text-based email clients.

Info

When editing HTML content, the plain text version is automatically updated, based on the content provided.

### [Scripting Language](/docs/mdces3/configuration/banners#scripting-language)

It is also possible to additionally customize templates using the **Handlebars** template scripting language. For more information see: <https://handlebarsjs.com/guide/>

### [Custom Fields](/docs/mdces3/configuration/banners#custom-fields)

The following field can be inserted into banner templates:

| Name | Description |
| --- | --- |
| First Name | Affected user's first name |
| Subject | Affected email subject |
| From | Affected email From: address |
| To | Affected email To: address |
| Date | Affected email date/time |
| Verdict | Policy verdict |
| Engines | Number of MetaScan™ Multiscanning engines used to scan content |
| Detected engines | Number of MetaScan™ Multiscanning engines that triggered the policy verdict |
| Action URL | Link to end-user actions wizard |

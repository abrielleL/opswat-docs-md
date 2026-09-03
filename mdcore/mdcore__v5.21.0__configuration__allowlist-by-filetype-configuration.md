<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/allowlist-by-filetype-configuration -->

# Allowlist by filetype configuration

## [Overview](/docs/mdcore/v5.21.0/configuration/allowlist-by-filetype-configuration#overview)

The **Allowlist File Type** feature allows you to skip scanning entirely for files of specific types. When a file matches an allowlist rule, it is immediately marked as **Whitelisted** (allowed) and **no scan engines are run on it**. The file receives a clean verdict without being scanned.

You can access this feature from the **Allowlist** tab in the workflow/rule configuration page.

> **Important:** Allowlisting means the file is trusted and bypasses all scanning. Use this only for file types you are confident do not need inspection.

---

Info

Since version 5.18.0, MetaDefender Core introduces a brand-new UI. To align with the updated UI/UX, some minor logic and usability changes have been implemented.

Previously, users were required to select a group first and then choose file types within that group, which made the feature less intuitive. In the updated version, the boundary between groups and file types has been streamlined. While groups are still maintained for backend alignment, users can now directly input file types when adding new items, making the process significantly more user-friendly.

There is also a slight change in UX behavior:

- **Before:** If a user enabled a group, selected specific items, and later disabled the entire group, those sub-items would remain configured when the group was re-enabled.
- **After:** Starting from version 5.18.0, if a group is disabled, all sub-items within that group are cleared. When the group is re-enabled, users will need to reselect the desired items.

Please note that this change only affects the user experience. The underlying logic remains unchanged—when a group is disabled, its sub-items are not applied, so there is no impact on backend processing or final results.

## [How It Differs from Blocklist](/docs/mdcore/v5.21.0/configuration/allowlist-by-filetype-configuration#how-it-differs-from-blocklist)

The allowlist is simpler than the blocklist — there is no mode selector (no "Block All" / "Block All Except"). You simply add file types that should be trusted and skip scanning.

| Feature | Blocklist | Allowlist |
| --- | --- | --- |
| **Purpose** | Prevent specific file types from being processed | Trust specific file types and skip scanning |
| **Verdict when matched** | Blocked | Whitelisted |
| **Scan engines run?** | No | No |
| **Modes** | Block All / Block All Except | Single mode (add trusted types) |
| **Archive-related option** | Allow In Archive / Allow Child Files | Ignore In Archive |

## [UI Controls](/docs/mdcore/v5.21.0/configuration/allowlist-by-filetype-configuration#ui-controls)

The Allowlist File Type dialog provides:

- **Search bar** - Filter the list of configured rules by file type name or extension.
- **Add Rule** button - Add a new file type rule.
- **Save** / **Cancel** buttons - Save your changes or discard them.

The table columns are:

| Column | Description |
| --- | --- |
| **File Type** | The file type to allowlist (e.g., "Adobe Files: PDF"). |
| **File Size Condition** | Optional size-based narrowing of the rule. |
| **Ignore In Archive** | Toggle to control whether this rule applies to files found inside archives. |
| **Action** | Delete the rule. |

## [Adding a Rule](/docs/mdcore/v5.21.0/configuration/allowlist-by-filetype-configuration#adding-a-rule)

1. Click **Add Rule**
2. A new row appears in the table (on top)
3. Select a **File Type** from the dropdown (e.g., "Adobe Files: PDF", "Image Files: JPEG").
4. Optionally configure a **File Size Condition** (see below).
5. Optionally toggle **Ignore In Archive** (see below).
6. Click **Save** to apply.

To remove a rule, click the trash icon in the **Action** column.

Info

After saving and closing the window, reopening it will display the items reordered alphabetically (grouped accordingly). However, you can easily locate configured items using the search bar, ensuring quick access to your settings.

---

## [File Size Condition](/docs/mdcore/v5.21.0/configuration/allowlist-by-filetype-configuration#file-size-condition)

Works the same as in the blocklist. Each rule can optionally include a file size condition to narrow when the allowlist rule applies.

**To enable:**

1. Toggle the **File Size Condition** switch to ON (blue).
2. Select a condition:

   - **If smaller than** - Only allowlist files smaller than the specified size.
   - **If bigger than** - Only allowlist files bigger than the specified size.
3. Enter a numeric value.
4. Select the unit: **B** (bytes), **KB** (kilobytes), or **MB** (megabytes).

**Examples:**

| Configuration | Effect |
| --- | --- |
| PDF + "If smaller than 5 MB" | PDF files under 5 MB are allowlisted (skip scanning); larger PDFs are scanned normally |
| JPEG + (size condition OFF) | All JPEG files are allowlisted regardless of size |

**Note:** When the file size condition is OFF, the rule applies to all files of the selected type regardless of size.

## [Ignore In Archive](/docs/mdcore/v5.21.0/configuration/allowlist-by-filetype-configuration#ignore-in-archive)

This option controls whether the allowlist rule applies to files found **inside an archive** (extracted files).

| Ignore In Archive | Behavior |
| --- | --- |
| **OFF** (default) | The allowlist rule applies to all matching files, whether they are uploaded directly or extracted from an archive. Both are marked as Whitelisted. |
| **ON** | The allowlist rule is **ignored** for files extracted from archives. Only directly uploaded files of this type are allowlisted. Extracted files proceed through normal scanning. |

**Why would you use this?**

When you trust a file type as a standalone upload (e.g., you trust directly uploaded PDFs from your users), but you still want to scan that same file type when it is embedded inside an archive. Archives can be used to disguise malicious content, so scanning extracted files provides an extra layer of security.

**Example scenario:**

1. You add a rule: Allowlist "Adobe Files: PDF" + Ignore In Archive = ON.
2. A user uploads `report.pdf` directly -> **Whitelisted** (skips scanning, clean verdict).
3. A user uploads `package.zip` containing `invoice.pdf` -> The ZIP is processed normally. When `invoice.pdf` is extracted, the allowlist rule is **ignored** because it came from an archive. The PDF proceeds through normal scanning by all configured engines.

**Another example (Ignore In Archive = OFF):**

1. You add a rule: Allowlist "Image Files: JPEG" + Ignore In Archive = OFF.
2. A user uploads `photo.jpg` directly -> **Whitelisted**.
3. A user uploads `images.zip` containing `photo.jpg` -> The extracted `photo.jpg` is also **Whitelisted** (the rule applies everywhere).

## [Searching Configured Rules](/docs/mdcore/v5.21.0/configuration/allowlist-by-filetype-configuration#searching-configured-rules)

Use the **search bar** at the top of the dialog to filter rules that have already been configured. Type a file type name or extension (e.g., "PDF", "Image", "JPEG") and the list will filter to show only matching rules.

## [Error section](/docs/mdcore/v5.21.0/configuration/allowlist-by-filetype-configuration#error-section)

The Errors section will automatically disappear once all issues have been resolved.

Clicking the **“Show All Errors”** button will filter the list to display only rows containing errors. In this view, the Blocklist Condition field, Add Rule option, search field, and Save button will be disabled. The button label will also change to **“Show All Rules.”**

Clicking **“Show All Rules”** will restore the full list and re-enable all previously disabled controls, returning the interface to its normal state.

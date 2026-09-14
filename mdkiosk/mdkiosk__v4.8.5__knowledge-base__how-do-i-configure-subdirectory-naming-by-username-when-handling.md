<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-configure-subdirectory-naming-by-username-when-handling -->

# How do I Configure Subdirectory Naming by Username When Handling Blocked or Allowed Files?

This article applies to all MetaDefender Kiosk releases deployed on Windows.

When using the feature to handle **Blocked** or **Allowed** files by sending them to a secondary directory, the UI provides limited options for naming subfolders — such as by **Session ID**, **Start Time**, or by **preserving the original structure**.

If your Kiosk is integrated with Active Directory (AD) and you want to automatically create subdirectories named after the logged-in username, follow the instructions below.

### [**Steps to Configure Username-Based Subdirectories**](/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-configure-subdirectory-naming-by-username-when-handling#steps-to-configure-username-based-subdirectories)

Add the following variable to define the subdirectory naming:

HtmlCopy%%%username%%%

**Example:** If the logged-in user is `user1`, files will be copied to:

HtmlCopy<Your Base Directory>/user1/

This subdirectory will be created automatically during file handling.

### [**Folder Permission Settings**](/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-configure-subdirectory-naming-by-username-when-handling#folder-permission-settings)

You can define the access control behavior for these subdirectories:

- **Inherited**: The subdirectory will inherit permissions from the parent folder.
- **Restricted**: Only the AD user who created the subdirectory will have access to it. Other users will be denied access.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

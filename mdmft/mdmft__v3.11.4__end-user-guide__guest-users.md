<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/end-user-guide/guest-users -->

# Guest Users

Summarize Page    Connect to Cursor Connect to VS Code

If MetaDefender Managed File Transfer™ is configured to allow guest account creation, you can create temporary guest accounts with limited permissions and lifetime.

Other users can share files with guests, but guests can only upload files to their own or their account creator's storage.

### [Creating Guest Users](/docs/mdmft/v3.11.4/end-user-guide/guest-users#creating-guest-users)

1. Go to the "Users" menu and select "Guest Users."
2. In the "Add New Guest User" window, set the following:

   - **Username:** A friendly name for the guest user
   - **Email**: The guest user's email for notifications
   - **Expiration time:** the date and time the account will expire (may be disabled depending on settings)

1. A special randomly generated Guest ID will created, which can be used for login. This Guest ID can be copied on the Guest Users page by opening the three-dot-menu and clicking on the 'Copy Guest ID' button.

Info

If an email address is provided properly during guest user creation, the guest user will receive a welcome message with a link to MetaDefender® MFT the ID for [signing in](/docs/mdmft/v3.11.4/end-user-guide/sign-in-as-guest-user).

Username must be between 3 and 30 characters long and can only contain alphanumeric characters(A-Z, 0-9), dots(.), spaces( ), dashes(-), pluses(+) and underscores(_). The special characters should not be put consecutively, at the end or beginning. Please try a different nickname.

3. Click "Add user" to finish creating a guest account.

Info

An email address can be shared among multiple guest accounts.

#### [Multi-MFT](/docs/mdmft/v3.11.4/end-user-guide/guest-users#multi-mft)

If Multi-MFT is enabled, multiple target MFTs can be selected, allowing the guest to be invited to and synchronize files across these MFTs.

---

### [Managing Guest Users](/docs/mdmft/v3.11.4/end-user-guide/guest-users#managing-guest-users)

To manage guest users, go to the "Users" menu and select "Guest Users."

The three-dot menu offers the following options:

- **Edit:** Allows you edit the **expiration date** (may be disabled depending on settings), change the **username** or the **email address**
- **Copy Guest ID:** Copies the guest user ID to the clipboard
- **Disable/Enable:** Disables the account to prevent login or enables it again
- **Delete:** Deletes the guest account if it is no longer needed

<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management -->

# Enterprise - SSH Access Management

The **SSH Access Management** setting is accessible under **Settings > SSH Access Management.**

The **SSH Access Management** module is designed to provide secure, time-bound, and IP-restricted SSH access to specific system components, such as the *Enterprise* environment. It offers fine-grained control for administrators and developers to manage SSH sessions efficiently.

- You need an **SSH key pair** (public and private).
- If you don’t have one, you can generate it on your machine

### [1. **Component Listing**](/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management#1-component-listing)

- Displays a list of system components: Enterprise Manager with SSH access configured.
- Columns include:

  - **MD OTS Component**: Enterprise
  - **SSH Public Key** status
  - **Allowed Access IPs**
  - **Allowed Access Period (Component Time)**
  - **Enable** toggle

### [2. **Enable/Disable SSH Access**](/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management#2-enabledisable-ssh-access)

- A toggle switch is provided per component.
- When **enabled**, users can configure SSH access details.
- Disabling the toggle immediately revokes SSH access for the selected component.

### [3. **Edit SSH Session Dialog**](/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management#3-edit-ssh-session-dialog)

Clicking the edit button opens a form to configure SSH session settings:

#### [**3.1. Component**](/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management#31-component)

- Non-editable field displaying the name of the selected component (e.g., Enterprise).

#### [**3.2. Enable SSH Access**](/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management#32-enable-ssh-access)

- Toggle to allow or block SSH access configuration.

#### [**3.3. SSH Public Key (Required)**](/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management#33-ssh-public-key-required)

- Upload the .pub file (public key) for authentication.
- Only valid public keys will be accepted.

#### [**3.4. Allowed Access IPs (Required)**](/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management#34-allowed-access-ips-required)

- Input or select IP addresses from which SSH access is allowed.
- Yellow advisory message: If you have a firewall, gateway, etc., please allow the following IP addresses.

#### [**3.5. Allowed Access Period (Component Time) (Required)**](/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management#35-allowed-access-period-component-time-required)

- Choose the allowed session period based on the component’s server time.
- Ensures time-restricted access for better security.

#### [**3.6. Current Component Time**](/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management#36-current-component-time)

- Displays current server time (e.g., May 13th 2025, 14:39:17).

#### [**3.7. Corresponds to User Time**](/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management#37-corresponds-to-user-time)

- Intended to show the local time equivalent for reference (not currently populated).

#### [**3.8. Save / Cancel**](/docs/md-ot-security/v.3.4.8/settings/enterprise-ssh-access-management#38-save--cancel)

- **Save:** Confirms and stores the configuration.
- **Cancel:** Discards changes and closes the dialog.

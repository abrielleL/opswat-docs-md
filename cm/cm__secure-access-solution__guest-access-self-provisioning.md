<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/guest-access-self-provisioning -->

# Guest Access Self Provisioning

## OVERVIEW

The RADIUS NAC Guest Access Module provides a self-provisioning user portal to allow guests to request and receive credentials to access the Guest Network without helpdesk involvement.

Provisioning Profiles allow administrators to configure which information users will be required to provide in order to receive their credentials from the RADIUS NAC system. This information includes valid email address, full name, reason for requested access, mobile phone number and mobile phone carrier. The email address or mobile phone number is required to deliver the credentials to the user. If this information is not authentic, they will have no way to receive their credentials and thus, no way to access the guest network.

## END USER EXPERIENCE

### Self-Provisioned Guest Access Overview

The guest user starts out by connecting to the network and is directed to an authentication page with information about guest access.

![](https://uploads.developerhub.io/prod/97qW/cil7crf251ztqsohtkmtah1p0j5ycbyo4swiu9740tznk917wycww1rvte98jwao.png)

In this scenario, the guest user clicks on the ‘Register’ button and is redirected to an registration portal:

![](https://uploads.developerhub.io/prod/97qW/wd4b16b0fvzckaxj4t8mqefkthutsq8ms87z9gm2pdqdupo49j77olakm0031b7n.png)

The guest user fills out the registration form, providing a valid E-mail, Name, and then clicks on the ‘Register’ button.

The guest user is redirected to a page notifying them about how their login credentials will be validated and a validation will be sent to them via email.

![](https://uploads.developerhub.io/prod/97qW/82u09qanetic75d51b59pzyef67loglckdyk831cd1vhvcvjha7plkdl4xc43tcd.png)

![](https://uploads.developerhub.io/prod/97qW/niow56fqdcdhoffs7q1s6cpo4fcmaod15j8cdysyw018zbr3eb7im08gf2n97sho.png)

Once the guest user activate their credentials, they can return to the authentication page and login.

## GUEST MANEGEMENT

The **Guest Users** tab shows all enrollment requests. Administrator can take any action Invite/edit/delete guest users in this screen.

Status available for Guest are: Approved, Denied, Pending approval. By default, after guest user submit a registration form will have the status as Pending approval.

## GUEST REGISTRATION SETTING

![](https://uploads.developerhub.io/prod/97qW/8ao8ktqlddo5rh4u0jnt22xmqiofkfe3c9pc7xc2ni9liv0gryarhtsrsyhzji7o.png)

### Global Settings

In this screen, Administrator will be able to manage guest access by enabling or disabling the self-registration option for visitors. When enabled, guests can independently register themselves to access the network.

### Registration Form

Administrators can customize Registration Form and control which fields are required, optional, or hidden, depending on their organization's security and data collection policies.

- **Email and Password** fields are fixed as required, ensuring a basic level of user identification and security.
- Additional fields such as **Full Name**, **Phone Number**, and **Reason for Access** can be customized to either be required, optional, or completely hidden from the form.

### Account Lifecycle

The **Account Lifecycle** section allows Administrators to define the duration of guest network access once their account is activated. This setting controls how long a guest account remains valid before requiring re-authentication or expiration.

- **Never Expire:** Selecting this option grants guests unlimited access, meaning their session will not expire unless manually revoked.
- **Expire In :** Administrators can set a specific expiration period, measured in days, hours, and minutes. Once this period ends, the guest will need to sign in again to regain access. This provides a controlled and time-limited access window for guests, enhancing security by automatically expiring access after the predefined time frame.

### Guest Validation Mode

When setting up guest access to your network, you have four convenient options to match your security needs and administrative preferences.

### 1. **Auto-approval**

**How it works:**

- Guest creates an account and verifies their email
- Account becomes immediately active - no waiting!
- Guest can connect right away using their registered credentials
- No administrator notification is sent
- Administrators can still manage these accounts through the Guest User Management Page

### 2. **Auto-approval with Admin Notification**

**How it works:**

- Guest creates an account and verifies their email
- Account becomes immediately active
- Administrator receives an email notification about the new account
- Guest can connect right away using their registered credentials
- Administrators can manage these accounts through the Guest User Management Page

### 3. **Admin Approval Required**

**How it works:**

- Guest creates an account and verifies their email
- Account remains inactive with "Pending Approval" status
- Administrator receives an email notification with approve/decline options
- Guest must wait for administrator approval before accessing the network
- Administrator can also approve accounts directly from the Guest User Management Page
- After approval, guest connects using their registered credentials

### 4. **Sponsor Approval Required**

**How it works:**

- Guest creates an account and enters their sponsor's email address
  - The sponsor email must match the Email Domain configured by Administrator
  - Example: If ".company.com" is the configured domain, sponsor email must end with "@company.com"
- Guest verifies their own email
- Account remains inactive with "Pending Approval" status
- Designated sponsor receives an email notification with approve/decline options
- Guest must wait for sponsor approval before accessing the network
- Administrators retain ability to manage accounts through the Guest User Management Page
- After approval, guest connects using their registered credentials

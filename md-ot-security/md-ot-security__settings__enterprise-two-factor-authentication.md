<!-- source: https://www.opswat.com/docs/md-ot-security/settings/enterprise-two-factor-authentication -->

# Enterprise - Two-factor Authentication

Two-factor Authentication is a way of verifying a user’s identity by using a combination of two different verification methods. It adds an extra layer of security, thereby ensuring that only authorized users can access an account, even if the password has been compromised.

In MD OT Security, the two methods used for two-factor authentication are:

- Username and password (normal login credentials)
- One-time security code via the **Authenticator** app

## [Enable Two-factor Authentication](/docs/md-ot-security/settings/enterprise-two-factor-authentication#enable-two-factor-authentication)

To enable Two-factor Authentication for your account, log in to your MD OT Security account and perform the following steps:

### [**1. Go to My Account → Two-factor Authentication (2FA)**](/docs/md-ot-security/settings/enterprise-two-factor-authentication#1-go-to-my-account--two-factor-authentication-2fa)

Click on your profile name on the top right-hand side of the page and select **Profile**. Then, choose the Two-Factor Authentication (2FA) change button.

Or navigate to **Settings** → **My Account → Two-factor Authentication (2FA)**

### [**2. Set up 2FA**](/docs/md-ot-security/settings/enterprise-two-factor-authentication#2-set-up-2fa)

Under **Two-factor Authentication**, clicking on the **Setup 2FA** button

### [3. Download Google Authenticator or another Authenticator app on your mobile device. See Google and Apple App Stores](/docs/md-ot-security/settings/enterprise-two-factor-authentication#3-download-google-authenticator-or-another-authenticator-app-on-your-mobile-device-see-google-and-apple-app-stores)

This method supports verification via the **Authenticator app** (available for iOS, Android, and Desktop). To use this method, you need to first install the application on your mobile phone or desktop PC and complete the registration using the same credentials as your MD OT Security. After selecting the Authenticator app, your MD OT Security account will be automatically registered with the app. It will then generate a security token, which you need to enter for verification.

### [4. Download the Recovery Code](/docs/md-ot-security/settings/enterprise-two-factor-authentication#4-download-the-recovery-code)

Store it in a safe place. This is a backup method allowing you to log in, if the app fails (2FA is deactivated when using Recovery Codes).

### [5. Scan the QR code](/docs/md-ot-security/settings/enterprise-two-factor-authentication#5-scan-the-qr-code)

Scan the QR code with your authenticator app or directly input the provided **Secret code** into your Authenticator app.

After that, the app will display a 6-digit code. Please enter it below for verification.

### [6. Complete 2FA setup](/docs/md-ot-security/settings/enterprise-two-factor-authentication#6-complete-2fa-setup)

Select **Continue**. With this step, two-factor authentication is enabled for your account.

### [7. Log in with 2FA](/docs/md-ot-security/settings/enterprise-two-factor-authentication#7-log-in-with-2fa)

Log out of your MD OT Security account. Log in again by entering your username and password. The next screen will prompt you to enter the Authentication code.

Or use the recovery code

## [Disable Two-Factor Authentication](/docs/md-ot-security/settings/enterprise-two-factor-authentication#disable-two-factor-authentication)

You can disable the Two-factor Authentication in a few steps. However, it is important to note that doing this will remove the additional layer of security from your account. MD OT Security highly recommends keeping it enabled.

Here are the steps for disabling two-factor authentication:

1. Go to the "Two-factor Authentication" page.
2. Click the "Disable 2FA" button

3. On the dialog box that appears, confirm by clicking on "Disable 2FA”

Once two-factor authentication is disabled, you will be able to log in to your account by simply entering your username and password.

## [Reset Two-Factor Authentication](/docs/md-ot-security/settings/enterprise-two-factor-authentication#reset-two-factor-authentication)

Once Two-factor Authentication is enabled. If you do not have access to your **Authenticator app** (if you changed it or otherwise), it won’t be possible to log in. Thankfully, MD OT Security has a way around this.

Here’s the process to reset two-factor authentication:

1. Go to the "Two-Factor Authentication" page.
2. Click the "Reset" button

3. Setup again

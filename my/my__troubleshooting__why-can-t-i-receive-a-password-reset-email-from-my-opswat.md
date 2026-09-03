<!-- source: https://www.opswat.com/docs/my/troubleshooting/why-can-t-i-receive-a-password-reset-email-from-my-opswat -->

# Why Can't I Receive a Password Reset Email from My OPSWAT?

You requested a password reset for your My OPSWAT account but did not receive the reset email.

## Possible reason 1: The email may be mistakenly flagged as spam or quarantined

| Term | Details |
| ---- | ---- |
| Problem | Can't I Receive a Password Reset Email from My OPSWAT after clicking "Forgot password" |
| Cause | The password reset email is sent from [**noreply@opswat.com**](mailto:noreply@opswat.com) with the subject line **"Reset My OPSWAT Account Registration."** However, in some cases, strict email policies may cause this email to be mistakenly flagged as spam or quarantined by your email security gateway. |
| Solution | 1. **Check Your Spam/Junk Folder:** - Search for an email from [noreply@opswat.com](mailto:noreply@opswat.com) with the subject "**Your Request to Change Password**." 2. **Check Your Email Security Gateway:** - If your organization uses an email filtering system, verify whether the email has been quarantined or blocked. 3. **Whitelist OPSWAT’s Email Domain:** - Add **asend.opswat.com** to your email allow list to prevent future filtering issues. 4. **Repeat the Password Reset Request:** - Go to **My OPSWAT Login Page** and request a password reset again after ensuring the email is not blocked. |

![](https://uploads.developerhub.io/prod/JYvy/smc3p8qlma6f5yxorp1wkw8dozp1ont0lheq49mst7wqbazzo16ln74nkm4vl3an.png)

## Possible reason 2: The email has not been registered in the Portal

| Term | Details |
| ---- | ---- |
| Problem | Cannot sign in My OPSWAT Portal. System shows "Your login attempt has failed. Make sure the email and password are correct." message, then user clicks "Forgot password" but the Reset password email is not send |
| Cause | The email has not been used to register any account |
| Troubleshooting | My OPSWAT Portal cannot show clearly that the user has inputted an incorrect email due to the privacy data rule. User must double-check and make sure the user has registered an account by this email or not. |
| Solution | Register My OPSWAT Portal by the email |

![](https://uploads.developerhub.io/prod/JYvy/mdgr6o3pqy6l393cp3rlkczg8pa4o69hft7ojnuevwf7ic8z03pp24uu93fm1cdz.png)

If the issue persists, please contact [OPSWAT Support](https://my.opswat.com/support) for further assistance.

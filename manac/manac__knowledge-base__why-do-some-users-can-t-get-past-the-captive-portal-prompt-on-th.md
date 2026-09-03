<!-- source: https://www.opswat.com/docs/manac/knowledge-base/why-do-some-users-can-t-get-past-the-captive-portal-prompt-on-th -->

# Why can some users not get past the captive portal prompt on the Open network?

## [Scope](/docs/manac/knowledge-base/why-do-some-users-can-t-get-past-the-captive-portal-prompt-on-th#scope)

This document applies to the scenario where users are quarantined as expected for captive portal authentication on the Open network. They can load the authentication page, but cannot get their LDAP or Active Directory credentials to work.

## [Exemption](/docs/manac/knowledge-base/why-do-some-users-can-t-get-past-the-captive-portal-prompt-on-th#exemption)

Before troubleshooting or opening a Support case, it’s recommended to exempt the users experiencing the issue, except for one or a small number of devices to be used for testing.

For a small number of devices, this can be done on a per-device basis in the Device Manager. Add each device to Open Access by MAC address and set an expiration time that leaves room for troubleshooting and resolution of the issue.

## [Troubleshooting](/docs/manac/knowledge-base/why-do-some-users-can-t-get-past-the-captive-portal-prompt-on-th#troubleshooting)

Each of these steps can be addressed in whatever order is most convenient for end users and the technical team.

- **Username format** - In some environments, the directory server will be looking for something other than a plain `username`. Try `user@domain` or `DOMAIN\user` instead.
- **Password rotation** - Many directory servers are configured to require users to reset their passwords periodically. Try resetting the user’s password.
- **Account lockout** - The user may have tried a bad combination of credentials to many times and too quickly. This can result in the account being locked out for a few minutes or longer, sometimes until manually reset. Try reactivating the use’s account on the directory server.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).

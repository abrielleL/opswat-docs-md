<!-- source: https://www.opswat.com/docs/ocm/7.39.0/troubleshooting/unable-to-login-to-opswat-central-management-with-setup-wizard-c -->

# Unable to login to OPSWAT Central Management with setup wizard credentials

| Term | Detail |
| --- | --- |
| Problem | Unable to login into OPSWAT Central Management with username set during setup wizard |
| Cause | OPSWAT Central Management requires email instead of username as credentials for new users of version 7. |
| Troubleshooting | Using the correct username and password still returns the message "Invalid credentials!" |
| Solution | Use email and password as login credentials. |

For new users of version 7, OPSWAT Central Management requires a combination of email and password as login credential for the account created in the setup wizard. However, for returning users who have chosen to import data from OPSWAT Central Management version 5, the login credentials for the imported accounts must be a combination of username and password instead.

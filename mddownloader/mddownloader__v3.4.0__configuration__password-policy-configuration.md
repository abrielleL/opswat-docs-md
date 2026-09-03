<!-- source: https://www.opswat.com/docs/mddownloader/v3.4.0/configuration/password-policy-configuration -->

# Password Policy

Password Policy settings are accessible under **Settings > Security** tab .

Local users' password can be enforced to meet requirements set by administrators, which includes following constraints:

- **Enforce password policy:**

  - Determines the number of unique new passwords that must be associated with a user account before an old password can be reused
  - Range: [0-24]
  - Default: 0 (to disable enforcement)
- **Minimum password length:**

  - The least number of characters that can make up a password for a user account
  - Range: [0-8]
  - Default: 0 (to disable enforcement)
- **Password must meet complexity requirements:**

  - Determines whether passwords must meet a series of guidelines that are considered important for a strong password:
  - Default: unchecked

Info

At least 1 uppercase letter of European languages (A through Z) At least 1 lowercase letter of European languages (a through z).

At least 1 base 10 digits (0 through 9) At least 1 non-alphanumeric characters (special characters): (~!@#$%^&*_-+=`|(){}[]:;"'<>,.?/)

Info

Only the user that has an admin role can modify this setting

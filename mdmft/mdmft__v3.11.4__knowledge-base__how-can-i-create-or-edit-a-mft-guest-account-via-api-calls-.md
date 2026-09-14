<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/how-can-i-create-or-edit-a-mft-guest-account-via-api-calls- -->

# How can I create or edit a MFT Guest account via API calls?

Summarize Page    Connect to Cursor Connect to VS Code

Users have the possibility of creating or editing a Guest MFT User via API calls by observing the documentation links below and taking note of the restrictions in place (as mentioned below):

New Guest MFT account -<https://docs.opswat.com/mdmft/metadefender-mft#postcreate-a-guest-account>

Edit a Guest account - <https://www.opswat.com/docs/mdmft/metadefender-mft#putmodify-a-guest-account>

- through these endpoints, you can define; **pin_code** (guest identifier):
- The length can be min 6 max 255 characters
- cannot contain spaces.
- **display_name** (guest nickname):
- between 3 and 30 characters long
- can only contain alphanumeric characters (A-Z, 0-9), dots(.), spaces( ), dashes (-), pluses(+) and underscores(_)
- The special characters should not be put consecutively

Support:

If you encounter any issues or require further assistance, please contact OPSWAT support via My OPSWAT at: https://my.opswat.com/home

Our support team will be able to provide you with the necessary guidance and resolution for any license-related concerns.

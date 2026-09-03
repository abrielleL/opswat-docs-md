<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/does-managed-file-transfer-support-restricting-ad-groups-from-ac -->

# Does Managed File Transfer support restricting AD groups from accessing Managed File Transfer?

Summarize Page    Connect to Cursor Connect to VS Code

Active Directory groups or users belonging to AD groups can be restricted from being shared with a file by denying them access to MetaDefender Managed File Transfer.

To deny access:

1. Go to "Managed File Transfer Settings" → "Active Directory" → "Configure"
2. In STAGE 5, include the *security groups* that require access

3. Exclude the security group that should not be shared with a file.

4. Finish the setup.

List of available groups to share a file with:

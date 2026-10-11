<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/what-is-the-difference-between--mft-to-mft--and--mft-pull--confi -->

# What is the difference between "MFT to MFT" and "MFT Pull" configurations?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [MFT to MFT use case](/docs/mdmft/v3.11.5/knowledge-base/what-is-the-difference-between--mft-to-mft--and--mft-pull--confi#mft-to-mft-use-case)

MFT to MFT is a system-level mirroring functionality. When enabled, all files transfer, folders creation, and user creation operations will be sent from the source MetaDefender Managed File Transfer to the destination MetaDefender Managed File Transfer server(s).

- This can also be set up with multiple target MFT servers, unlike the MFT Pull job, which needs to be configured individually for each target MFT.

By setting up and integration both MFT systems simultaneously this way, this ensures redundancy for all file and folder actions.

For more details on how to configure MFT to MFT and the supported mirrored operations, please read our documentation on [MFT to MFT](/docs/mdmft/v3.11.5/configuration/vault-to-vault).

## [MFT Pull use case](/docs/mdmft/v3.11.5/knowledge-base/what-is-the-difference-between--mft-to-mft--and--mft-pull--confi#mft-pull-use-case)

MFT Pull is a user-level job, thus MFT Pull files jobs will only pull files from the configured sources for the users who have defined such jobs.

Each individual user can configure their own MFT Pull jobs, if they have the role "[Automation coordinator](/docs/mdmft/v3.11.5/operating/RBAC-role-base-access-control-permissions)". When configuring, each user will need to provide their own credentials, to access and pull files that are owned by them, or shared with them, from the source MFT instance to the current MFT instance.

- The MFT Pull job can also be used without automation, only triggered on-demand during file uploads by [Enabling Pulling on Upload Files](/docs/mdmft/v3.11.5/configuration/pull-mft#pull-files).

By configuring MFT Pull jobs, users can transfer files from a low-security network to a high-security network in a secure manner, by initiating the transfer from the MFT instance located in the high-security network.

For more details, please read our documentation on [MFT Pull](/docs/mdmft/v3.11.5/automated-file-transfer/mft---pull-files).

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support).

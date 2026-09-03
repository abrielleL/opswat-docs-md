<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/quarantine -->

# Quarantine

## [Options](/docs/mdcore/v5.21.0/configuration/quarantine#options)

The quarantine is for keeping blocked files in a separated place. It can be used by configuring workflows (see [Advanced](/docs/mdcore/v5.21.0/configuration/workflow-configuration-template#advanced) configuration for the Workflow Template).

On the **Quarantine** page (**History → Quarantine**), the following operations can be performed on the quarantined files:

1. By clicking on the ... item, details appear.
2. Pinned files won't be removed on clean-ups. Use the pin icon to do so.
3. For removing the files from the list, please use the bin icon.
4. Files can be downloaded by clicking the download icon.

The *Check with Adaptive Sandbox, Check with SBOM,* the *Pin*, *Unpin* and *Delete* operations can also be performed in bulk using the check boxes before the filenames and clicking the action icons above the file list.

Check with Adaptive Sandbox

Files in the quarantine can be uploaded to Adaptive Sandbox to retrieve deep analysis result.

This feature requires the **Adaptive Sandbox** technology to be licensed, and enabled in workflow.

Quarantine items may be sent to Adaptive Sandbox:

1. Manually select the file and click on the `Check with Adaptive Sandbox`button, or
2. Automatically, driven by the configuration under [Quarantine settings](/docs/mdcore/v5.21.0/configuration/quarantine#quarantine-settings)

## [Check with SBOM](/docs/mdcore/v5.21.0/configuration/quarantine#check-with-sbom)

Files in the quarantine can be uploaded to SBOM engine to retrieve deep analysis result.

This feature requires the **SBOM** technology to be licensed, and enabled in workflow.

Quarantine items may be sent to SBOM:

1. Manually select the file and click on the `Check with SBOM`button, or
2. Automatically, driven by the configuration under [Quarantine settings](/docs/mdcore/v5.21.0/configuration/quarantine#quarantine-settings)

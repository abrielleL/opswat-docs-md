<!-- source: https://www.opswat.com/docs/mdcore/configuration/my-opswat-central-management -->

# My OPSWAT Central Management

On this session, we will introduce how to enroll MetaDefender Core (MD Core) into My OPSWAT Central Management (MOCM) version 10, configure MD Core on MOCM, and the settings related to the connection between MD Core and MOCM.

Supported modes

✅ **Standalone DB mode**: since MD Core v5.14.0.

🟨 **Shared DB mode**: starting from MD Core v5.18.0 with a few limitations.

### [Limitations when enrolling shared-mode MD Core with MOCM v10](/docs/mdcore/configuration/my-opswat-central-management#limitations-when-enrolling-shared-mode-md-core-with-mocm-v10)

#### [Certificate Management Limitation](/docs/mdcore/configuration/my-opswat-central-management#certificate-management-limitation)

Per MOCM enrollment protocols, certificates synchronized from MOCM should remain non-deletable within MD Core. However, in certain shared-mode deployments where multiple MD Core instances are enrolled with MOCM, unenrolling a single instance may inadvertently allow those certificates to be deleted from the remaining enrolled MD Cores.

#### [Group Configuration Limitation](/docs/mdcore/configuration/my-opswat-central-management#group-configuration-limitation)

Shared-mode and standalone-mode MD Cores cannot coexist within the same MOCM Group Policy configuration.

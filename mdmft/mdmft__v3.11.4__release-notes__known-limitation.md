<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/release-notes/known-limitation -->

# Known Limitation

Summarize Page    Connect to Cursor Connect to VS Code

- Re-enabling the admin user using the **UpdateCredentials** tool may result in a licensing-related error. Please refer to the [guide](/docs/mdmft/v3.11.4/knowledge-base/updatecredentials-tool---cannot-re-enable-users) for proper steps.
- MetaDefender Vault is not FIPS-compliant when upgrading from version v2.0.8 or below to v2.0.9 or above. Only new deployments starting from v2.0.9 or above can run with FIPS-enabled mode.
- When .NET Framework 4.8 is not present the installation might require a computer restart in order to complete or make sure that the latest updates are installed using Windows Update
- When a computer restart is required on Windows Server 2019 the installer may not be able to trigger the restart operation at the end due to an OS limitation. Please use one of the following solutions:

  - Restart the machine manually at the end of the installation
  - Run the installer as administrator
  - Assign the "Shut down the system" permission on local security policy, sign out and sign in, then launch the installer. The permission inheritance from the 'Administrators' group is not enough
- Generating new encryption key from version v3.6.0 till 3.7.2 results in a state that MFT-to-MFT functionality cannot be used. To recover from this state please contact support.

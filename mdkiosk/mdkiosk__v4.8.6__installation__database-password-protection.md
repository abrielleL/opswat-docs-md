<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/installation/database-password-protection -->

# Database password protection

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The KIOSK database is password-protected to safeguard sensitive customer information and ensure secure KIOSK operations.

Each KIOSK has a unique database password, accessible only by the KIOSK services on that specific system. The password is generated using three components:

- Hardware information specific to that KIOSK.
- A KIOSK security salt.
- User input provided during installation, adding an optional extra layer of security as outlined in [Installing MetaDefender Kiosk Using the Install Wizard](/docs/mdkiosk/v4.8.6/installation/installing-metadefender-kiosk-using-the-install-wizard).

Info

The password is created once and retained during KIOSK upgrades.

The database password and the user-input encrypted key are both hashed and securely stored for internal usage at:

- `C:\ProgramData\OPSWAT\Metadefender\blue`
- `C:\ProgramData\OPSWAT\Metadefender\green`

Warning

Missing these files can lead to a critical failure of the KIOSK, as the system will be completely unable to authenticate to the database.

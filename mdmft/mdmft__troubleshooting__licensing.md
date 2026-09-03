<!-- source: https://www.opswat.com/docs/mdmft/troubleshooting/licensing -->

# Supported Calendar types

Summarize Page    Connect to Cursor Connect to VS Code
### [License Activation Failed Due to Unsupported Calendar Type](/docs/mdmft/troubleshooting/licensing#license-activation-failed-due-to-unsupported-calendar-type)

If you encounter a license activation issue, ensure your system is set to the Gregorian calendar. Follow these steps to configure this setting in Windows.

1. #### [Change Regional Format to a Gregorian Calendar Region](/docs/mdmft/troubleshooting/licensing#change-regional-format-to-a-gregorian-calendar-region)

Info

Skip this step if system accounts are using a different regional format that the current user.

- Go to "Start" → "Control Panel"
- Under the "Clock and Region" section select “Change date, time, or number formats”
- Select a region that uses the Gregorian calendar by default

2. Copy Settings

Info

Skip this step if system accounts are using a different regional format that the current user.

- In the "Administrative" tab select "Copy settings..."
- Check “Welcome screen and system accounts”
- Click "OK"

3. Change Regional Format to Desired Region with Gregorian and Non-Gregorian Calendar Options

- Go to "Start" → "Control Panel"
- Under the "Clock and Region" section select “Change date, time, or number formats”
- Choose a region with both Gregorian and non-Gregorian calendar options

4. Copy Settings

- Go to "Administrative" tab
- Select "Copy settings..." and “Welcome screen and system accounts”

5. Restart MetaDefender Managed File Transfer Services

- Go to "Start" → "Control Panel" → "Services"
- Restart the "OPSWAT MetaDefender Managed File Transfer Helper" service

6. Activate License

After restarting the MFT services, go to the "License Activation" page and attempt to activate your license again.

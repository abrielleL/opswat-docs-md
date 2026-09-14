<!-- source: https://www.opswat.com/docs/netwalldiode/v1.13.2/configuration/diode-backup -->

# Backups

A backup or snapshot is a copy of your Optical Diode configurations and data. The Optical Diode creates a backup automatically before all configuration changes are made. You can also make a backup on demand.

You will perform all backup tasks from the Backup Configs pane. Open the **Configuration** menu and click **Backups** to access this pane, which displays the following information for the current backups:

- **Description**: The appliance makes a description for automatic backup that includes the date and time of the backup. For manual backups, the description comes from the Comment box.
- **Created**: Timestamp in the format of Weekday:MM:DD: HH:MM:SS YYYY
- **Name**: The system supplies the name. You cannot change it.

### [Create a Backup](/docs/netwalldiode/v1.13.2/configuration/diode-backup#create-a-backup)

1. Open the **Action** menu and click **Snapshot Running Config**. A popup displays, “Snapshot (backup) the current config?”
2. Enter a comment that includes the cause for the backup. This text becomes the description on the *Backup Configs* pane.
3. Click the **Submit** button to save the backup. A green banner at the top of the page tells you the procedure succeeded.

### [Export a Backup](/docs/netwalldiode/v1.13.2/configuration/diode-backup#export-a-backup)

Double-click the backup you want to export. A detail page displays.

1. Open the **Action** menu and click **Export**. The *Backup Config Export* pane displays.
2. Enter the **Password** for this backup. Enter the password again in the **Confirm Password** box. Record the password in a safe place.
3. Click the **Submit** button. A popup page displays. **Open** the file or **Save** it. If you save it, the file goes to your local Downloads location. The default location for Windows systems is *C:\Users<your user name>\Downloads*.

### [Restore a Backup](/docs/netwalldiode/v1.13.2/configuration/diode-backup#restore-a-backup)

If a new configuration does not operate correctly, you can return an older configuration (rebuild). You can select a backup of this appliance or upload a configuration from a different appliance.

1. To use a backup from a different appliance, save the backup to a location on this NetWall server network:

   1. To upload the software to the appliance, open the **Action** menu and click **Upload**. The *Upload* pane displays.
   2. Click **Browse** in the *_Local Filename of config *_box to navigate to the file. Record the name.
   3. Enter a **Password** for this backup.
   4. Click the **Upload Config** button to start the upload. The **Progress Bar** shows when the upload completes.
   5. This backup shows in the Backup Configs table.

Find the backup name in the Backup Configs table. You can click a column header to filter the table contents.

If the window is full screen, the **Action** menu is the last column in the Backup Configs table and click **Apply** in the row for the backup.

[If the window is smaller, the **Action** menu is a **plus sign (+)** in the first column. Click the **+ sign** and then click **Apply**.](If the window is smaller, the **Action** menu is a **plus sign (+)** in the first column. Click the **+ sign** and then click **Apply**.)

### [Delete a Backup](/docs/netwalldiode/v1.13.2/configuration/diode-backup#delete-a-backup)

1. Find the backup in the **Backup Configs** table. You can click a column header to filter the table contents.

Click the backup row to open a detail page.

Open the **Action** menu and click **Delete**. Click the **Submit** button to confirm your action. A green banner at the top of the page tells you that the procedure succeeded.

MetaDefender

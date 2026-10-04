<!-- source: https://www.opswat.com/docs/mddrive/v4.4.9/troubleshooting/extract-logs -->

# Extract Log Files

On Linux systems, you can manually extract a collection of the most recent log files:

1. Insert MetaDefender Drive into the target device and run a file browser as an admin using the `sudo` command.
2. Navigate to the /*persistence* folder in MetaDefender Drive partition and copy the logs files from the following folders:

- From the */media/your_user_account/persistence/rw/opt/ometadefender-drive* folder: copy the *Log* folder.
- From the */media/your_user_account/persistence/rw/var* folder: copy the *crash* and *log* folders.

Log file location for manual extraction

.

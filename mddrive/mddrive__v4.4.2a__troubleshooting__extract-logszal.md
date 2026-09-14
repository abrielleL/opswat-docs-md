<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/troubleshooting/extract-logszal -->

# Generate a Drive Image

As an alternative to generating support packages and extracting log files, a MetaDefender Drive image can be generated from a Linux machine via terminal commands.

### [Generate a MetaDefender Drive Image](/docs/mddrive/v4.4.2a/troubleshooting/extract-logszal#generate-a-metadefender-drive-image)

1. Insert the MetaDefender Drive that you want to clone into a running Linux machine.
2. Launch the terminal, and run the following command:

lsblk -o name,serial,mountpoint

3. Identify the drive you want to clone by the `serial` value, then copy its `name`. In the sample image below, the drive to be cloned is `/dev/sdb`

A Linux terminal window showing all the mounted Drives

4. Run the following command after replacing`/dev/sdx` with your drive's `name` and `/path/to/img/Drive.img.gz4` with the filesystem location and the file name where you want the image saved.

sudo dd if=/dev/sdx bs=1024 status=progress | gzip -c > /path/to/img/Drive.img.gz4. fd

.

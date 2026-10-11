<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-to-scan-clonezilla-images-with-kiosk -->

# How to scan Clonezilla images with Kiosk

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Starting from version 4.7.7, Kiosk support scanning Clonezilla image.

## [Prerequisites](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-scan-clonezilla-images-with-kiosk#prerequisites)

During the preprocessing and enumeration phase, each folder is checked to determine whether it is a Clonezilla folder. A valid Clonezilla folder must meet the following conditions:

1. **Required files**: The folder contains `clonezilla-img`, `disk, parts`, and`Info-img-id.txt.`
2. **Disk file**: The `disk`file contains a single line specifying the disk name (e.g., *sda*, *sdb*).
3. **Parts file**: The `parts`file lists partition names on a single line, separated by spaces. Partition names are formed by the disk name followed by a number (e.g., *sdb1 sdb2 sdb4*).
4. **Disk metadata**: The following files must exist for the identified disk: `DISKNAME-pt.parted`,`DISKNAME-mbr`, `DISKNAME-gpt-1st`, and`DISKNAME-gpt-2nd`.
5. **Disk data**: Partition data files must follow the format `**PARTITION.FILESYSTEM-ptcl-img.***` , where `PARTITION` *is a partition name and* FILESYSTEM *is the file system type (e.g.,* `sdb1.xfs-ptcl-img.gz.aa`).

## [Configurations](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-scan-clonezilla-images-with-kiosk#configurations)

From Kiosk Console, navigate to Configuration > Advanced > Disk Image Settings > Clonezilla

- Scan full disk: Kiosk scans the entire disk, including the original file and all child files contained within
- Scan Original files: Kiosk scans only the original file, without processing child files

## [How does Kiosk scan the Clonezilla folder](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-scan-clonezilla-images-with-kiosk#how-does-kiosk-scan-the-clonezilla-folder)

Once the Kiosk detected a folder as a valid Clonezilla folder, it will proceed with preprocessing and mounting process

1. Restore the Clonezilla folder to Raw disk image

   1. Kiosk uses the built-in`clonezilla-util` to convert the partition data files into a raw partition image. For example, the `sdb1.xfs-ptcl-img.gz.aa` is converted to `sdb1.img`.
   2. Next, Kiosk combines with `-mbr, -gpt-1st, ...` files to produce the raw disk image `sdb.img`
2. Convert the raw disk to VHDX file using `qemu-img`
3. The VHDK file will then be mounted by Windows as usual. The Paragon software will also be used to read the uncommon Linux file systems such as XGS and BTRFS

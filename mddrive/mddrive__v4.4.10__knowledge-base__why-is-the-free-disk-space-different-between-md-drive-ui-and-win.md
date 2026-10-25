<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/knowledge-base/why-is-the-free-disk-space-different-between-md-drive-ui-and-win -->

# Why is the free disk space different between MD Drive UI and Windows Explorer?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Drive USB has a total capacity of 64 GB, which is divided into **two equal partitions**::

1. **NTFS partition**: This partition is used to store the scan reports and logs. It is visible and accessible in Windows Explorer, where it appears as a regular drive.
2. **Ext4 partition**: This partition contains the MetaDefender Drive's Linux operating system and temporary working directory. It is *not* visible in Windows Explorer. Over time, particularly after performing long scans or scanning large archive files, this partition may become full as the temporary space is used up. You can monitor its usage in the MetaDefender Drive UI under **Settings > Preferences > Storage**. If the EXT4 partition becomes nearly full, you will see a warning message when booting into MetaDefender Drive:`"Disk is almost full. Used: X%"`. Please note that **you cannot free up space in this partition using Windows Explorer**. The only way to clean up this partition is by clicking the **Clean-up** button in the MD Drive UI.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-to-resolve-disk-partition-visibility-issues-caused-by-omva- -->

# How to resolve Disk Partition visibility issues caused by OMVA?

This article applies to all OMVA versions lower than 2.0.9 deployed on Windows.

### [Problem Summary:](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-resolve-disk-partition-visibility-issues-caused-by-omva-#problem-summary)

On Windows system, the OPSWAT OMVA agent caused an issue where Disk Management could not list disk partitions.

The OMVA agent version older than **2.0.9** introduced a compatibility issue with Windows Disk Management. This interference prevented the system from recognizing disk partitions, leading to backup application failures.

The issue was resolved in OMVA agent version **2.0.9 or later**, which restored compatibility with Disk Management.

### [Resolution Steps: Upgrade OMVA Agent to Version 2.0.9](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-resolve-disk-partition-visibility-issues-caused-by-omva-#resolution-steps-upgrade-omva-agent-to-version-209)

1. Download the latest OMVA agent (v2.0.9) from your MetaDefender Kiosk console management
2. On the affected Windows system:

   - Uninstall the existing OMVA agent.
   - Install the OMVA version **v2.0.9** or later
3. Reboot the system after installation to ensure the changes take effect.
4. Confirm that Disk Management now properly lists all disk partitions.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

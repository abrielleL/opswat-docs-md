<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/can-md-kiosk--windows--scan-split-vmdk-files- -->

# Can MD Kiosk (Windows) scan split VMDK files?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

In specific situations some customers might determine (based on log entries) that MD Kiosk (Windows) does not support VMDK type files that have been split up.

They might experience log entries similar to the examples listed below:

Meta Defender Kiosk **can definitely handle** the case of split VMDK files.

What the user sees in the log is simply that MD Kiosk will try to mount all VMDK found because there is no easy way to tell if somebody purposely rename the file B.vmdk to A-s001.vmdk (in hope of it getting skipped when scanning).

For a real split VMDK, mounting the main file A.vmdk automatically ‘combines’ all the constituent files A-s001.vmdk , A-s002.vmdk, …

Support:

If you encounter any issues or require further assistance, please contact OPSWAT support via My OPSWAT at: https://my.opswat.com/home

Our support team will be able to provide you with the necessary guidance and resolution for any license-related concerns

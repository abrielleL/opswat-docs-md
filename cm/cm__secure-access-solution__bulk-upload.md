<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/bulk-upload -->

# Bulk Upload

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

My OPSWAT Central Management provides administrators with the ability to add up to 1,000 addresses to a **SSH, RDP, or Other** protected application.

There are two methods for adding the addresses:

1. **Manually**: By selecting the **+Add an Address**, a new address field will appear and a user can add a valid IPv4 or IPv6 address, IP range, CIDR block, or domain in the field.

2. **Bulk Upload**: By selecting the upload button (☁) , users can select to either replace or add to their address list. My OPSWAT Central Management will only accept .txt files with up to 1,000 addresses.

   1. If there are any typos in the uploaded .txt file, My OPSWAT Central Management will notify the user and will require those be amended prior to upload.
   2. If there are any duplicated addresses, My OPSWAT Central Management will remove the duplicates during the upload process.

When administrators are done adding addresses, they can continue with creating or updating the protected application.

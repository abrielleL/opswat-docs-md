<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/does-adding-a-second-mft-in-the-kiosk-serve-as-a-high-availabili -->

# Does adding a second MFT in the Kiosk serve as a high-availability mechanism?

The feature allowing the addition of multiple MFTs (Managed File Transfers) in the Kiosk is not intended as a high-availability mechanism. Here’s a detailed explanation of how this functionality works.

The option to configure multiple MFTs in the Kiosk is designed to support different workflows. It allows users to assign specific MFTs to individual workflows based on requirements.

Adding a second MFT does not create a high-availability setup. There is no failover mechanism to switch to the secondary MFT if the primary MFT becomes unavailable.

Similarly, the Kiosk does not support a round-robin approach for load balancing between MFTs. Each workflow must explicitly select which MFT it uses, and the system will not automatically alternate between them.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).

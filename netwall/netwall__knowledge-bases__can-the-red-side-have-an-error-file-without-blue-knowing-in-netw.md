<!-- source: https://www.opswat.com/docs/netwall/knowledge-bases/can-the-red-side-have-an-error-file-without-blue-knowing-in-netw -->

# Can the Red Side Have an Error File Without Blue Knowing in NetWall USG?

This article applies to NetWall USG all versions.

NetWall USG ensures secure, one-way data transfer from a sender (Blue network) to a receiver (Red network). This design uses specialized PCIe cards that provide a complete protocol break, ensuring no direct network connection between Blue and Red.

A common question is: *“What happens if the Red side fails to receive a file? Can Blue still know the transfer status?”*

The answer is Yes — Blue will always know whether Red successfully received the file. Below is how the mechanism works.

**How the File Transfer Mechanism Works**

1. File Transmission

   - The Blue (sender) system sends the file across the USG to the Red (receiver) system.
2. Red-Side Acknowledgment

   - If the Red system successfully receives the file, it records that status in a shared memory segment on the Red side.
3. Blue-Side Status Check

   - The Blue system cannot receive any direct data back from Red.
   - Instead, Blue periodically fetches the transfer status from the shared memory segment.
   - This ensures Blue knows whether the file was successfully retrieved by Red.
4. One-Way Enforcement

   - No data ever flows from Red → Blue.
   - Only the status flag (success/failure) is accessible to Blue, and Blue must actively pull it.

**Security Benefits**

- The USG uses PCIe cards to enforce physical separation and break the network protocol.
- Since only status flows back (not data), the risk of compromise from Red → Blue is eliminated.
- This mechanism guarantees transfer status synchronization without exposing Blue to Red network traffic.

**Key Takeaway**

If a file transfer fails on the Red side, Blue will not be left unaware. The USG’s memory-segment mechanism ensures Blue can always check whether Red successfully received the file.

So, regarding the question: “Can the Red side still have an error file without Blue knowing?” → No. Blue will always know the transfer result.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-do-i-receive-kiosk-license-mismatch-error- -->

# Why do I receive Kiosk License mismatch error?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

When attempting to license MD Kiosk and encountering the "License Mismatch" error, it indicates that there is a discrepancy between the provided license and the Deployment ID associated with the machine. The Deployment ID is a unique identifier generated for each machine during the licensing process.

The error commonly occurs when the Deployment ID of the machine was generated incorrectly or has become outdated. To resolve this issue, a simple procedure can be followed:

1. Rename the machine to a random name: By changing the machine's name, we trigger a change in the system's identification.
2. Restart the machine: The restart ensures that the new machine name is applied and the necessary system components are updated accordingly.
3. Rename the machine back to its original name: After the restart, revert the machine's name to its original value.
4. Restart the machine again: This additional restart forces the Deployment ID generating algorithm to recalculate the Deployment ID based on the updated machine name.

By following these steps, the system generates a fresh and accurate Deployment ID that aligns with the provided license. This effectively resolves the "License Mismatch" error and allows the licensing process to proceed smoothly.

It's worth noting that the exact procedure may vary depending on the specific software or system being used. However, the fundamental principle remains the same: by modifying the machine name, restarting the machine, and then restoring the original name followed by another restart, we trigger the recalculation of the Deployment ID, ensuring its alignment with the provided license.

Remember to consult the software's documentation or reach out to the appropriate support channels for any specific instructions or troubleshooting steps related to the licensing process.

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).

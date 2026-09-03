<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-do-i-find-all-the-mft-logs-and-its-functionality- -->

# How do I find all the MFT logs and their functionality?

Summarize Page    Connect to Cursor Connect to VS Code

All service logs are located at:

PathCopyC:\Program Files\OPSWAT\MetaDefender Managed File Transfer\Services\Logs

1. **Helper Service (OPSWAT MetaDefender Managed File Transfer Helper)**: Ensures other services, including Nginx, are running. Errors can be found in *opswat.mft.helper.service.log*.
2. **Next Service (OPSWAT MetaDefender Managed File Transfer Next)**: Manages REST API services for newer endpoints (e.g., automated jobs). Errors can be found in *opswat.mft.next.service.log*.
3. **Processor Service (OPSWAT MetaDefender Managed File Transfer Processor)**: Handles background tasks (e.g., core scanning, data retention). Errors can be found in *opswat.mft.processor.service.log*.
4. **Rest Service (OPSWAT MetaDefender Managed File Transfer REST)**: Main API service for most features of MetaDefender Managed File Transfer™. Errors can be found in *opswat.mft.rest.service.log*.

Other Logs:

1. **Nginx as a Reverse Proxy**: Nginx acts as a reverse proxy for MetaDefender Managed File Transfer™ by routing client requests to backend services. Errors can be found in: *C:\Program Files\OPSWAT\MetaDefender Managed File Transfer \WebServer\logs.*
2. **Installer logs**: Error logs related to the MetaDefender Managed File Transfer™ installation process are stored in:

- For new versions:

PathCopyC:\Users\<username>\AppData\Local\Temp\OPSWAT\MetaDefender Managed File Transfer\mft.log

- For old versions:

PathCopyC:\Users\<username>\AppData\Local\Temp\OPSWAT\MetaDefender Vault\vault.logSupport

If further assistance is required, please submit a [Support Ticket](https://www.opswat.com/support) with the OPSWAT team.

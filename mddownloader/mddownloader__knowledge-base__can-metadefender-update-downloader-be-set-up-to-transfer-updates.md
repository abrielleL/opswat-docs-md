<!-- source: https://www.opswat.com/docs/mddownloader/knowledge-base/can-metadefender-update-downloader-be-set-up-to-transfer-updates -->

# Can MetaDefender Update Downloader Be Set Up to Transfer Updates to OPSWAT Central Management via FTP?

Yes, MetaDefender Update Downloader can support FTP transfer to OPSWAT Central Management Server, but it is not recommended due to security purposes.

Security Considerations

FTP (File Transfer Protocol) is an outdated and insecure method for transferring files due to several vulnerabilities, including:

1. Lack of Encryption: FTP transfers data, including credentials, in plain text, making it susceptible to interception and unauthorized access.
2. Passive and Active Mode Risks: FTP operates in both passive and active modes, both of which can introduce security risks such as port exposure and susceptibility to man-in-the-middle attacks.
3. No Integrity Verification: FTP does not provide built-in mechanisms for verifying data integrity, increasing the risk of tampered updates being transferred.
4. Limited Access Control: FTP does not support modern authentication mechanisms, making it harder to enforce strict security policies.

To ensure secure and reliable communication, OPSWAT Central Management requires the use of secure protocols such as HTTPS or SFTP for transferring updates. These protocols provide encryption, authentication, and data integrity verification, aligning with modern security best practices.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).

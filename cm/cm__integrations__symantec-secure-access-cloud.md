<!-- source: https://www.opswat.com/docs/cm/integrations/symantec-secure-access-cloud -->

# Symantec Secure Access Cloud

This guide shows you how My OPSWAT Central Management can be easily and seamlessly integrated into Symantec Secure Access Cloud (TM) to implement Zero Trust Network architecture when accessing any corporate resource deployed in any datacenter (on-premises or in a private or public cloud) from any device. [Learn more.](https://support.symantec.com/us/en/article.tech254810.html)

By integrating My OPSWAT Central Management to Symantec Secure Access Cloud (TM) , administrators are able to check remote devices for:

- **Vulnerabilities -** Detect vulnerabilities on endpoints in installed applications and operating systems.
- **Enhanced Compliance** - Get greater visibility into the status of installed security applications such as hard disk encryption and system information such as password protection to ensure devices are compliant with existing policies.
- **Unwanted Applications** - Detect and remove non-compliant or unwanted applications such as peer-to-peer applications from a remote device.
- **Advanced Threat Detection** - Utilizing two methods of advanced threat detection, My OPSWAT Central Management helps identify potential threats that existing anti-malware software might not protect against.
- **Portable media scanning and access control** - Protect organizations against threats from portable media on the endpoints, a common attack vector for malware.
- **Anti-screen capture** - Prevent keyloggers and advanced malware from accessing sensitive data.
- **Screen capture protection** - Prevent unauthorized or accidental screenshots and recording by users, VDI, web collaboration tools, and malicious applications.

Documents:

- Guideline: [https://knowledge.broadcom.com/external/article?articleId=174934](https://knowledge.broadcom.com/external/article?articleId=174934)

You can set up a My OPSWAT Central Management account to manage up to 50 devices with free of charge. [Start Trial Now](https://go.opswat.com/communityRegistration?app=0sp1a000000GmuY&startURL=%2Fidp%2Flogin%3Fapp%3D0sp1a000000GmuY%26binding%3DHttpPost%26inresponseto%3Da514j14ag33h8jf1030acdgjfcgab9)

**Notes:**

- If your devices sit behind a firewall or a proxy, you need to allowlist domains to make sure devices are able to talk to My OPSWAT Central Management cloud. See more details at [How do I configure MetaDefender Endpoint to work with a proxy or outbound firewall?](https://www.opswat.com/docs/cm/knowledge-base/how-do-i-configure-metadefender-endpoint-to-work-with-a-proxy)
- You need to enable Cross-domain API settings (Settings > Integrations) on your account at the port 11639 and please make sure that there is no application which used the port 11369 on your endpoints.

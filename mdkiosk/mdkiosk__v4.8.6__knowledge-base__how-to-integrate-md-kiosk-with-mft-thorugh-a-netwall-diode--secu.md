<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-to-integrate-md-kiosk-with-mft-thorugh-a-netwall-diode--secu -->

# How to integrate MD Kiosk with MFT thorugh a Netwall diode/ Secure gateway?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### [Introduction](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-integrate-md-kiosk-with-mft-thorugh-a-netwall-diode--secu#introduction)

This document describes how to integrate MetaDefender Kiosk with MetaDefender MFT by routing traffic through an OPSWAT NetWall data diode. The objective is to ensure a one-way, policy-enforced data transfer from the MetaDefender Kiosk (blue side) to MFT (red side) while preserving security boundaries.

Scope: Configure Kiosk to use the Blue NetWall as the MFT endpoint, set up matching unilateral HTTP(S) streams on NetWall (Blue and Red) using the same channel, and validate successful uploads end-to-end.

Assumptions: You have administrative access to MetaDefender Kiosk, NetWall (both sides), and MFT; IP addressing is reachable or appropriately routed; and you can create and manage API keys in MFT.

Security considerations: Use HTTPS where possible with trusted certificates; restrict source/destination addresses on NetWall streams; and limit API key scope and lifetime per your security policy.

Success criteria: Kiosk connectivity check passes (green check), files scanned on Kiosk are delivered to MFT.

**MFT Diode Upload Wait**

Since a data diode only allows one-way communication (no return acknowledgment channel), after uploading each file to MFT via a diode (*Synchronize with Data Diode* enabled), Kiosk sleeps 10 seconds by default before continuing (configurable via registry `HKLM\SOFTWARE\OPSWAT\MD4M\sft_upload_wait_seconds`, in seconds) — this gives the diode time to fully process one HTTP request before the next is sent, since sending requests too close together can cause it to drop/mishandle them and silently fail uploads on larger file batches.

#### [Prerequisites](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-integrate-md-kiosk-with-mft-thorugh-a-netwall-diode--secu#prerequisites)

MFT: Create a system-level API key in Settings → Security → API Keys with a sensible expiration (default is 1 hour).

Reference addresses (example):

- Kiosk: 10.1.0.1:8009
- Blue NetWall: 10.10.0.2
- Red NetWall: 10.20.0.2
- MFT: 10.2.0.1:8010

#### [1) Configure Kiosk to talk through Blue NetWall](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-integrate-md-kiosk-with-mft-thorugh-a-netwall-diode--secu#1-configure-kiosk-to-talk-through-blue-netwall)

1. Set MFT URL in Kiosk to the Blue NetWall address: https://10.10.0.2:8010/vault_rest

Use the MFT API key created above. A green check confirms validity.

2. Certificates:

- Configuration → Advanced → Certificate handling: import the NetWall certificate if required, or temporarily disable SSL verification during testing.

3. Workflow setting:

In Allowed files → Copy to secondary location → MFT, enable Synchronize with Data Diode

#### [2) Blue NetWall (ingress, from Kiosk)](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-integrate-md-kiosk-with-mft-thorugh-a-netwall-diode--secu#2-blue-netwall-ingress-from-kiosk)

Create a Stream → HTTP with:

- Channel: pick one (e.g., 3). Must match Red.
- Type: Unilateral
- Name: e.g., KIOSK TO MFT
- Protocol: HTTP
- Port: 8010 (must match Kiosk’s MFT URL port)
- Source address: 10.1.0.1 (Kiosk IP)
- Enabled: On

If MFT uses HTTPS:

- Advanced → Encryption → SSL/TLS credentials → Actions → Import key pair; then select it and Submit.

If Kiosk is in a different subnet:

- Advanced → Networking → L3 Routes → Add L3 Route
- Destination: e.g., 10.1.0.0/24 (Kiosk subnet)
- Gateway: Blue NetWall gateway, e.g., 10.10.0.254

#### [3) Red NetWall (egress, to MFT)](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-integrate-md-kiosk-with-mft-thorugh-a-netwall-diode--secu#3-red-netwall-egress-to-mft)

Create a Stream → HTTP with:

- Channel: same as Blue (e.g., 3)
- Type: Unilateral
- Name: e.g., KIOSK TO MFT
- Protocol: HTTP
- Port: 8010 (same as Blue/Kiosk config)
- Destination address: 10.2.0.1 (MFT IP)
- Encryption SSL: Enabled if MFT uses HTTPS
- Enabled: On

#### [4) Result](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-integrate-md-kiosk-with-mft-thorugh-a-netwall-diode--secu#4-result)

With the above in place, Kiosk will upload scanned files to MFT through the OPSWAT Data Diode (Blue → Red).

#### [Quick checklist](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-integrate-md-kiosk-with-mft-thorugh-a-netwall-diode--secu#quick-checklist)

- MFT API key created; non-1h expiry set.
- Kiosk MFT URL points to Blue (https://<Blue-IP>:8010/vault_rest) + API key works (green check).
- Kiosk cert trust set (or temporary SSL verify disabled for test).
- Kiosk workflow → Synchronize with Data Diode enabled.
- Blue NetWall unilateral HTTP stream: src 10.1.0.1, port 8010, Channel N.
- Red NetWall unilateral HTTP stream: dst 10.2.0.1, port 8010, same Channel N.
- If cross-subnet, Blue L3 route added (e.g., 10.1.0.0/24 via 10.10.0.254).
- If HTTPS, NetWall SSL/TLS key pair imported and selected.

#### [Troubleshooting tips](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-integrate-md-kiosk-with-mft-thorugh-a-netwall-diode--secu#troubleshooting-tips)

Kiosk test fails (no green check):

- Verify API key validity/expiry in MFT.
- Confirm Kiosk URL points to Blue IP, correct port 8010 and /vault_rest.

No traffic seen on Red:

- Channel mismatch between Blue/Red streams; both must match (e.g., 3).
- Missing L3 route on Blue if Kiosk is remote subnet.

SSL errors:

- Import proper SSL/TLS key pair on NetWall (for HTTPS), or temporarily disable Kiosk SSL verification to isolate cert issues.

#### [Network Flow Diagram](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-integrate-md-kiosk-with-mft-thorugh-a-netwall-diode--secu#network-flow-diagram)

Support

If further assistance is required, please proceed to log a support case or chat with our support engineers: https://my.opswat.com/support

<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/sdp-cli--linux-only- -->

# SDP CLI (Linux Only)

## [SAML SSO](/docs/macloud-sdp/configuration---management/sdp-cli--linux-only-#saml-sso)

The most common use case is to do authentication via SAML SSO:

- Log into the IDP as normal. The administrator should have previously made the SDP app available to end-user.
- Select that app. If prompted, confirm the application to open the SDP app.

Note that launching the client with the the same authentication result twice may fail. Authentication tokens at the end of SAML can only be used once. If there are any issues signing in, try signing out of the IDP and back in.

Since the Linux client is CLI-only, there will be no immediate feedback that SDP has connected successfully. Checking the status manually can show where this is in the process:

BashCopysdp status

This command will notify the user that SDP is **connecting**, and then when it completes, SDP will show as **connected**.

## [Local Users](/docs/macloud-sdp/configuration---management/sdp-cli--linux-only-#local-users)

If the user is defined as an end-user directly in the MetaDefender IT-OT Access UI, they will need to use Cognito authentication.

BashCopysdp connect cognito -s STAGE_URL -a ACCOUNT -u EMAIL [ -p PASSWORD ]

e.g.

BashCopysdp connect cognito -s https://api-us.sdp.opswat.com -a AAAAAAAA -u example@example.com -p password

- `STAGE_URL` is which MA/Secure IT Access stage is being targeted.

  - For most customers this is probably [https://api-us.sdp.opswat.com](https://api-us.sdp.opswat.com/)
  - For customers in the EU this is probably <https://api-eu.sdp.opswat.com>
- `ACCOUNT` is the MetaDefender IT-OT Access registration code.

  - The registration code is listed in the MA UI under **Settings > Global > Account**
- `EMAIL` is the email of the user
- `PASSWORD` is required, but if omitted the user will be prompted at the command line such that the characters are obscured to avoid leaking plaintext passwords in the shell

If a default pool has not be set by the local user, the user will need to review the list of pools, and set their default pool.

Once the user tries to connect, they can see the most recent list of valid gateway pools they have access to via:

BashCopysdp listPools

This will return all valid pool values. To select one of those pools to connect to, the user will need to run:

BashCopysdp setPool -p <poolUUID>

After running this command, the user should be able to use the local cognito command to sign into SDP successfully.

## [Remediation Required](/docs/macloud-sdp/configuration---management/sdp-cli--linux-only-#remediation-required)

The most common error is that the user is not compliant with all configured MetaDefender IT-OT Access policies. This results in status messages like:

BashCopyFailure Reason=AccessBlocked

To correct, check the compliance status with the MetaDefender Endpoint. To trigger the remediation page:

BashCopyopswat-client -r

If there are any problems , reach out to the local administrator for assistance. They can help open a support case with OPSWAT.

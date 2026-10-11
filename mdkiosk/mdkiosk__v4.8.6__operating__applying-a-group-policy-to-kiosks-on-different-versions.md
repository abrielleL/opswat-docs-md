<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/operating/applying-a-group-policy-to-kiosks-on-different-versions -->

# Applying a Group Policy to Kiosks on Different Versions

View as Markdown Ask ChatGPT about this page Ask Claude about this page
# [Applying a Group Policy to Kiosks on Different Versions](/docs/mdkiosk/v4.8.6/operating/applying-a-group-policy-to-kiosks-on-different-versions#applying-a-group-policy-to-kiosks-on-different-versions)

Central Management can apply the same group policy to Kiosks that aren't all running the same MetaDefender Kiosk version. When a Kiosk in a managed group receives or inherits its group's policy, Central Management automatically adapts the policy's settings to match what that Kiosk's installed version supports, so administrators don't need to keep every device on the exact same version just to manage them together.

Note

Available starting with MetaDefender Kiosk 4.7.6. Kiosks on earlier versions should be upgraded before being added to a group managed under a shared policy.

## [How It Works](/docs/mdkiosk/v4.8.6/operating/applying-a-group-policy-to-kiosks-on-different-versions#how-it-works)

This works as follows:

- If the group policy includes a setting that doesn't exist yet on an older Kiosk's version, that Kiosk applies every setting it does recognize and records that one or more settings were not recognized — it doesn't fail to apply the rest of the policy.
- If a setting has been removed from newer versions of Kiosk but an older Kiosk in the group still has that setting configured, the older Kiosk keeps its current value instead of losing it.
- Kiosks on significantly older, unsupported versions do not receive policies intended for much newer versions at all — this avoids applying a policy that could put an outdated Kiosk into an inconsistent state. To manage such a Kiosk under the same group policy, upgrade it to a supported version first.

## [Prerequisites](/docs/mdkiosk/v4.8.6/operating/applying-a-group-policy-to-kiosks-on-different-versions#prerequisites)

- Central Management 10.x (CM10).
- MetaDefender Kiosk 4.7.6 or later on each device expected to receive a policy authored against a different, but supported, Kiosk version.
- Each Kiosk enrolled in Central Management and assigned to the group governed by the shared policy.

Note

This capability has no local Kiosk Console setting — a Kiosk in the supported version range participates automatically once enrolled and assigned to a group whose policy was authored against a different (but supported) Kiosk version.

<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/session-timeout -->

# Session Policy

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Session Policy settings are accessible under **Settings > Security** tab

- Idle session timeout: Idle timeout to invalidate individual user’s session based on that user last activity.
- Session timeout: Absolute timeout to invalidate individual user’s session regardless of that user activities.
- Allow Duplicate Sessions: Allow same user to have multiple active sessions.
- Allow Cross IP Sessions: Allow requests coming from sources different from the authenticated origin.

REST API for session timeout

Learn more at: [PUT - Session settings](/docs/mdcore/v5.22.1/metadefender-core#configsession)

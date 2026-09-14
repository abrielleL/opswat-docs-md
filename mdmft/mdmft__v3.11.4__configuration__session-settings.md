<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/session-settings -->

# Session Settings

Summarize Page    Connect to Cursor Connect to VS Code

### [Absolute Session Timeout Period](/docs/mdmft/v3.11.4/configuration/session-settings#absolute-session-timeout-period)

For example, with default values, a user who logs in at 9 AM would be able to stay signed in until 10 AM. If a file uploaded happens before 10 AM (i.e at 9:45 AM) the session is automatically extended until 10:45 AM.

This can happen over and over again until the user signs out (at which point the session is terminated) or a day has passed (default absolute timeout).

Absolute session timeout period can range from a minimum of 5 minutes to a maximum of 7 days.

Defines an absolute timeout for a session. A session is extended while the user interacts with the web application but will not be extended beyond the absolute timeout.

### [Idle Session Timeout Period](/docs/mdmft/v3.11.4/configuration/session-settings#idle-session-timeout-period)

Sets an idle timeout for user sessions. If there is no user interaction within this timeframe, the session expires, leading to an automatic logout.

- Example: If the idle session timeout is set to 1 hour, a user who logs in at 9 AM and leaves the application untouched until 10 AM will experience an expired session. Interaction with the application will extend the session until it reaches the absolute session timeout.

The idle session timeout has a minimum value of 1 minute and a maximum value of 2 hours.

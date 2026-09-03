<!-- source: https://www.opswat.com/docs/mdicap/configuration/session-timeout -->

# Session Timeout

Authenticated user session is invalidated via timeout which is now configurable on MetaDefender ICAP Server UI under Security screen (**Settings > Security > Session Policies**)

**Idle Timeout** (in minutes)

If there is no user activity, current session will become invalid after the given timeout.

- Value can be set in the range of [0, 120]

  - Default value is 5.
  - 0 means the idle timeout is disabled.

**Absolute Session Timeout** (in minutes)

Regardless of user activity, current session will become invalid after given timeout.

- Value can be set in the range of [0, 120]

  - Default value is 0.
  - 0 means the absolute timeout is disabled.

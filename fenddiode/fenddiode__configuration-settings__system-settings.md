<!-- source: https://www.opswat.com/docs/fenddiode/configuration-settings/system-settings -->

# System Settings

## [About](/docs/fenddiode/configuration-settings/system-settings#about)

- Model Number – Displays the diode model number.
- Serial Number – Displays the diode serial number.
- Firmware Version – Displays the current firmware version on the device.

## [Real Time Clock](/docs/fenddiode/configuration-settings/system-settings#real-time-clock)

- Sync – Synchronizes diode's RTC to workstation system time.

## [Power Failure](/docs/fenddiode/configuration-settings/system-settings#power-failure)

- Enabled – Enables or disables the power failure events tracking feature.
- Clear – Clears all recorded power events.
- Events – Lists all recorded power events.
- Clear Timer Every – The time in hours your diode will hold onto power failure event logs. When the timer expires, logged events are cleared.

  - [0-255, in hours; 0 means “Do not clear”]

## [Firmware Update](/docs/fenddiode/configuration-settings/system-settings#firmware-update)

- Browse – Opens a dialog box to select a firmware file.
- Update – Starts the firmware update process once a file has been selected.

## [Diagnostics](/docs/fenddiode/configuration-settings/system-settings#diagnostics)

- Mode – Sets diagnostic mode on or off. “Off” means no diagnostic information will be sent.
- Level of Info –Sets the verbosity (level of detail) of the diagnostic information as follows:

  - Info (1,2,3) – Displays info, warning, and error messages
  - Warning (2,3) –Displays warning and error messages
  - Error (3 Only) – The least verbose setting, displays only error messages
- Retry Timer – Sets how often the diode will attempt to connect with an external diagnostic server to send diagnostic messages.

  - [0-255, in seconds; 0 means “no retry”, as in the diode will only try to connect one time and if no connection is made or connection is lost, it will not retry]
- Target Server IP Address – Sets the IP address for the target diagnostic server that will receive diagnostic messages from the outbound side of the diode

  - [IP address in format: ###.###.###.###]
- Target Server Port Number (1-65535) – Sets the port number for the target diagnostic server that will receive diagnostic messages from the outbound side of the diode

  - [0-65535]

## [Configuration Session Settings](/docs/fenddiode/configuration-settings/system-settings#configuration-session-settings)

- Port Always On – When checked, the diode will always be available for a configuration session. When not check the diode will close the configuration port after the indicated length of time. If “always on” mode is not checked, you must physically power cycle the diode (using the reset button or by unplugging the diode and plugging it back in) to reopen the configuration port in order to log back into the diode to configure it.
- Port Timeout – When “Configuration Port Always On” is not checked, this field specifies the window of time you can connect to the diode before the diode closes the configuration port.
- Session Length – The duration of a configuration session. The default is 30 minutes.

  - [10-60 minutes]

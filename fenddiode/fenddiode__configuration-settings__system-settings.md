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

## [Remote Syslog](/docs/fenddiode/configuration-settings/system-settings#remote-syslog)

- Mode – Sets remote syslog reporting on or off. “Off” means no syslog will be sent.
- Level of Info – Sets the verbosity (level of detail) of the reported syslog. Selecting a higher number will include all messages for that number and all lower numbered message tiers (For example, selecting "2:Critical' will send alerts for levels 2, 1, and 0):

  - 0:Emergency
  - 1:Alert
  - 2:Critical
  - 3:Error
  - 4:Warning
  - 5:Notice
  - 6:Informational
  - 7:Debug
- Facility - Sets the reported facility for remote syslog. All syslog messages reported from the diode will report the same facility. Available facilities:

  - 0:kern
  - 1:user
  - 2:mail
  - 3:daemon
  - 4:auth
  - 5:syslog
  - 6:lpr
  - 7:news
  - 8:uucp
  - 9:cron
  - 10:authpriv
  - 11:ftp
  - 12:ntp
  - 13:security
  - 14:console
  - 15:solaris-cron
  - 16:local0
  - 17:local1
  - 18:local2
  - 19:local3
  - 20:local4
  - 21:local5
  - 22:local6
  - 23:local7
- Retry Timer – Sets how often the diode will attempt to connect the remote syslog server. Only applicable with a "Syslog Transport" of 'TCP'.

  - [0-255, in seconds; 0 means the diode will immediately reattempt to connect to the remote syslog server.]
- Target Server IP Address – Sets the IP address for the remote syslog server to which the output side of the diode will send syslog messages.

  - [IP address in format: ###.###.###.###]
- Target Server Port Number (1-65535) – Sets the port number for the remote syslog server to which the output side of the diode will send syslog messages.

  - [0-65535]
- Transport - Sets the operating mode for delivering syslog to the remote server. Both TCP and UDP are supported.

  - [UDP, TCP]

## [Configuration Session Settings](/docs/fenddiode/configuration-settings/system-settings#configuration-session-settings)

- Port Always On – When checked, the diode will always be available for a configuration session. When not check the diode will close the configuration port after the indicated length of time. If “always on” mode is not checked, you must physically power cycle the diode (using the reset button or by unplugging the diode and plugging it back in) to reopen the configuration port in order to log back into the diode to configure it.
- Port Timeout – When “Configuration Port Always On” is not checked, this field specifies the window of time you can connect to the diode before the diode closes the configuration port.
- Session Length – The duration of a configuration session. The default is 30 minutes.

  - [10-60 minutes]

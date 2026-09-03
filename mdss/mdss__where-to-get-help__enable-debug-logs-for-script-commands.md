<!-- source: https://www.opswat.com/docs/mdss/where-to-get-help/enable-debug-logs-for-script-commands -->

# Enable debug logs for script commands

In order to troubleshoot please run :

UnixWindowsCopysudo LOG_LEVEL=7 [mdss-command]PS> .\mdss.ps1 [mdss-command] -log_level=7

where **mdss-command** is the command that has an issue. For example, if MetaDefender Storage Security cannot be started please run the following command:

UnixWindowsCopysudo LOG_LEVEL=7 mdss -c startPS> .\mdss.ps1 -c start -log_level 7

<!-- source: https://www.opswat.com/docs/mdss/4.6.0/where-to-get-help/enable-debug-logs-for-script-commands -->

# Enable debug logs for script commands

In order to troubleshoot please run :

```bash
sudo LOG_LEVEL=7 [mdss-command]
```

```bash
PS> .\mdss.ps1 [mdss-command] -log_level=7
```

where **mdss-command** is the command that has an issue. For example, if MetaDefender Storage Security cannot be started please run the following command:

```bash
sudo LOG_LEVEL=7 mdss -c start
```

```bash
PS> .\mdss.ps1 -c start -log_level 7
```

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

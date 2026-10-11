<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/troubleshooting/tcp-ip-port-exhaustion -->

# TCP/IP Port Exhaustion

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Issue symptom](/docs/mdcore/v5.22.1/troubleshooting/tcp-ip-port-exhaustion#issue-symptom)

`Only one usage of each socket address (protocol/network address/port) is normally permitted` error appears in Nginx web server access log while MetaDefender Core is operating on Windows OS. There could possibly be a few reasons causing:

- Running out of available ports for new connections.
- Each closed port has a delay time (`WAIT_TIME`) before being re-used for another new connection, but in some cases, the delay time is too long. As the result we don't have port available for new connections.

## [Solution](/docs/mdcore/v5.22.1/troubleshooting/tcp-ip-port-exhaustion#solution)

### [A. Increasing port range](/docs/mdcore/v5.22.1/troubleshooting/tcp-ip-port-exhaustion#a-increasing-port-range)

On Windows, by default the number of available ports is 5000 and maximum can be set is 65534.

#### [1. Use command line](/docs/mdcore/v5.22.1/troubleshooting/tcp-ip-port-exhaustion#1-use-command-line)

Check how much port can be used by running command:

netsh int ipv4 show dynamicport tcp

Example output:

Protocol tcp Dynamic Port Range
---------------------------------
Start Port : 1024
Number of Ports : 64511

To adjust default values, use command:

netsh int ipv4 set dynamicport tcp start=<starting_range> num=<total_number>

Restart Windows OS to apply new settings

#### [2. Use registry](/docs/mdcore/v5.22.1/troubleshooting/tcp-ip-port-exhaustion#2-use-registry)

- Follow the path `HKLM\System\CurrentControlSet\Services\Tcpip\Parameters`
- Choose Edit → New → DWORD (32-bit) Value and enter `MaxUserPort`
- Right click and choose Modify on the new key
- Set your desired number
- Restart Windows OS to apply new settings

### [B. Decreasing TCP wait time](/docs/mdcore/v5.22.1/troubleshooting/tcp-ip-port-exhaustion#b-decreasing-tcp-wait-time)

Default value is 4 minutes and can be set to lower e.g. 30 seconds (***however, if you are using synchronous scan mode, then decreasing TCP wait time shall not be ideal***)

- Follow the path `KLM\System\CurrentControlSet\Services\Tcpip\Parameters` in Registry
- Choose Edit → New → DWORD (32-bit) Value and enter `TcpTimedWaitDelay`
- Right click and choose Modify on the new key
- Set number of seconds to wait (e.g. 30)
- Restart Windows OS to apply new settings

## [References](/docs/mdcore/v5.22.1/troubleshooting/tcp-ip-port-exhaustion#references)

- <https://docs.microsoft.com/en-us/troubleshoot/windows-server/networking/default-dynamic-port-range-tcpip-chang>
- <https://support.jda.com/articles/Question/What-does-the-error>

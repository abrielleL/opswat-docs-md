<!-- source: https://www.opswat.com/docs/mdcore/troubleshooting/too-many-time-wait-socket -->

# Too Many TIME_WAIT Socket

This trouble is **only on Linux** systems.

If TCP connections are in use the port limit can be reached. In this case, no new connection can be created.

## [How to detect](/docs/mdcore/troubleshooting/too-many-time-wait-socket#how-to-detect)

Kernel message:

kernel: TCP: request_sock_TCP: Possible SYN flooding on port 8009. Sending cookies. Check SNMP counters.

Check the `TIME_WAIT` sockets count:

watch -n 1 "netstat -nt | grep TIME_WAIT | wc -l"

If it is close to the available port range then your system is suffers from this issue:

cat /proc/sys/net/ipv4/ip_local_port_range
## [Solution](/docs/mdcore/troubleshooting/too-many-time-wait-socket#solution)

You should enable socket reusing.

By default Linux selects a port from an ephemeral port range, which by default is a set to range from 32768 to 61000.

A TCP local socket address that has been bound is unavailable for some time after closing, unless the `SO_REUSEADDR`flag has been set. Care should be taken when using this flag as it makes TCP less reliable.

To avoid waiting on closed sockets and enable reusing them set tcp_tw_reuse sysctl to enable reusing of `TIME_WAIT` sockets by appending the following line to file **/etc/sysctl.conf**:

net.ipv4.tcp_tw_reuse = 1

After this, sockets in state `TIME_WAIT` will be reused when necessary.

## [Technical Insights](/docs/mdcore/troubleshooting/too-many-time-wait-socket#technical-insights)

Connect function error value in these cases is `EADDRNOTAVAIL`.

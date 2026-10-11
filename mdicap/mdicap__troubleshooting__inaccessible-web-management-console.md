<!-- source: https://www.opswat.com/docs/mdicap/troubleshooting/inaccessible-web-management-console -->

# Inaccessible Web Management Console

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Connection refused or browser is waiting](/docs/mdicap/troubleshooting/inaccessible-web-management-console#connection-refused-or-browser-is-waiting)

The Web Management Console can not be accessed from browser. You get an error message (connection refused) or your browser is waiting for reply.

## [Solution](/docs/mdicap/troubleshooting/inaccessible-web-management-console#solution)

1. Please make sure your computer can access the MetaDefender ICAP Server IP address.
2. Please make sure you entered the correct URL into your browser.
3. Please make sure you opened the firewall port on the MetaDefender ICAP Server server for the Web Management Console. Consult your Linux Distribution manual on how to configure a firewall in your distribution.

## [Invalid license](/docs/mdicap/troubleshooting/inaccessible-web-management-console#invalid-license)

The Web Management Console can not be accessed from browser. You get the following message:

The problem is that:

- The MetaDefender ICAP Server license is not valid (not licensed at all or maximum client number is reached)
- The Web Management Console is accessed via a Proxy server or other ICAP client

## [Solution](/docs/mdicap/troubleshooting/inaccessible-web-management-console#solution)

Try accessing the Web Management Console directly from the machine that hosts the ICAP Server or with no Proxy connection.

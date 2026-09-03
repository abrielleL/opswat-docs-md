<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/troubleshooting/inaccessible-management-console -->

# Inaccessible Management Console

Problem: You cannot access the MetaDefender Core Management Console from your browser e.g. <http://localhost:8008>

## [Symptom](/docs/mdcore/v5.21.0/troubleshooting/inaccessible-management-console#symptom)

After you enter the Metadefender Core Management Console address (e.g. http://localhost:8008) you get an error message (connection refused) or your browser is waiting for reply.

## [Troubleshooting tips](/docs/mdcore/v5.21.0/troubleshooting/inaccessible-management-console#troubleshooting-tips)

1. Check if your computer can access the Metadefender Core IP address / domain name. Verify that you opened the firewall port on the Metadefender Core server for the Management Console.
2. Check if you are using proper protocol HTTP / HTTPS.
3. Check if you are using proxy for the connection.
4. Check if MetaDefender Core service is still running.
5. Check MetaDefender Core's Nginx web server log for a clue.

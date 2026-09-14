<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-troubleshoot-inaccessible-management-console -->

# How to Troubleshoot Inaccessible Management Console?

This knowledge base article provides step-by-step instructions for checking and resolving the issue when MetaDefender Core becomes unreachable after disabling HTTPS.

**Problem**: You cannot access the MetaDefender Core Management Console from your browser e.g. [http://localhost:8008](http://localhost:8008/)

**Symptom**: After you enter the Metadefender Core Management Console address (e.g. [http://localhost:8008](http://localhost:8008/)) you get an error message (connection refused) or your browser is waiting for reply.

**Steps to resolve the issue:**

- Check if your computer can access the Metadefender Core IP address / domain name. Verify that you opened the firewall port on the Metadefender Core server for the Management Console.
- Check if you are using proper protocol HTTP / HTTPS.
- Check if you are using proxy for the connection.
- Check if MetaDefender Core service is still running.
- Check MetaDefender Core's Nginx web server log for a clue.
- Sometimes the browser will autofill/cache the address and even if you are entering the URL manually with HTTP instead of HTTPS, the browser will still load the HTTPS, and thus the error message. To resolve this situation, you can either clear the browser history/cookies or use a different browser / computer to test the connection.

Once browser data has been cleared, the MetaDefender Core console can be accessed using the HTTP protocol without further issues.

Support:

If you encounter any issues during the activation process or require further assistance, please contact OPSWAT support via [My OPSWAT](https://my.opswat.com/portal/support).

Our support team will be able to provide you with the necessary guidance and resolution for any license-related concerns.

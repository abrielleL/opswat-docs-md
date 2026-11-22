<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-lms-activation -->

# License Management Server Activation

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Connect to License Management Server (LMS)](/docs/mdcluster/installation/md-cluster-lms-activation#connect-to-license-management-server-lms)

1. Sign in to MetaDefender Cluster **Control Center** console.
2. Go to `Library` > `Licenses` and select `License Management Server` tab.
3. Select `Activate` and provide the necessary information in the required fields of the `License Management Server (LMS) Activation` dialog:

   1. **Host URL**: The URL of the License Management Server to connect to.
   2. **REST Port**: The port of the License Management Server.
   3. **Token**: Access token obtained from the License Management Server.

4. After input all required fields, the connection to LMS will be established and available rules can be selected under `Rule`.

Info

The port number defined in "Maintain Socket Connectivity With LMS Through Port `<port_number>`" is required to sustain connectivity between MD Cluster Control Center and License Management Server. In order for successfully activation, **confirm that the port is properly configured and allowed in firewall setting**.

5. Select the appropriate rule and choose Activate. Upon successful completion, the license details will be shown.

Info

Once activation is successful, the License Management Server will manage the license status of all MetaDefender Core instances. Please ensure sufficient quota is available.

6. Check instance status under `Library` > `Workers` and confirm all MetaDefender Core instances is activated successfully.

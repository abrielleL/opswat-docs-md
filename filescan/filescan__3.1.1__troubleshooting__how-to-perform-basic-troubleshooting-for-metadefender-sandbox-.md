<!-- source: https://www.opswat.com/docs/filescan/3.1.1/troubleshooting/how-to-perform-basic-troubleshooting-for-metadefender-sandbox- -->

# How to perform basic troubleshooting for MetaDefender Aether?

MetaDefender Aether is a containerized application composed of multiple Docker containers that work in tandem to deliver full functionality. To begin troubleshooting, it is essential to assess the overall health and status of these containers.

**Step 1: Check Container Status**

To view all running and stopped containers, use the following command:

**sudo docker ps -a**

This command provides an overview of each container’s status, including creation time, current state, and uptime. This information is critical for identifying any containers that may have failed or are not running as expected.

**Step 2: Understand Key Components**

MetaDefender Aether is built on several core components:

- **Webservice**: The front-end interface of the platform.
- **Transform**: The engine responsible for file scanning and analysis.
- **Broker**: Facilitates communication between the webservice and the transform engine.

**Step 3: Review Logs**

Logs for each component are located at:

**/home/sandbox/sandbox/logs**

**Note**: Not all components log to a file right now, some of them are only available by checking the running docker containers. We do also provide a script to create a Support Package: [Collect logfiles](https://www.opswat.com/docs/filescan/2.3.0/troubleshooting/collect-logfiles)

Examine these logs to identify potential issues within each component:

- **Webservice Logs**: Investigate when the user interface is unresponsive or components fail to render correctly.
- **Transform Logs**: Useful for diagnosing scanning failures, timeouts, and erratic behavior such as jobs not processing correctly.
- **Broker Logs**: If both the webservice and transform containers appear healthy but scanning is still failing, the broker logs may reveal communication issues between the components.

Support:

If Further Assistance is required, please proceed to log a support case or chatting with our support engineer.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

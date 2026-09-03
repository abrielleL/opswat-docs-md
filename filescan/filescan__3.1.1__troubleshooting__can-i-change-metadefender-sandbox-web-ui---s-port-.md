<!-- source: https://www.opswat.com/docs/filescan/3.1.1/troubleshooting/can-i-change-metadefender-sandbox-web-ui---s-port- -->

# Can I change MetaDefender Aether Web UI’s port?

Yes, the port used by the MetaDefender Aether Web Interface can be modified.

The port mapping is defined in the following configuration file:

/home/sandbox/sandbox/webservice/docker-compose.nginx.yml

In this file, the port mapping follows the format:

**<external_port>:<internal_container_port>**

To change the external port accessed by users, simply modify the left-hand (external) port value. For example:

After updating the configuration, apply the changes by restarting the Sandbox application using the following script:

**/home/sandbox/sandbox/restart_sandbox.sh**

Once restarted, the MetaDefender Sandbox Web UI will be accessible at:

**https://<sandbox_ip>:12345**

This allows you to customize the web interface port to meet your network or security requirements.

Support:

If further assistance is required, please proceed to log a support case or chatting with one of our support engineers.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

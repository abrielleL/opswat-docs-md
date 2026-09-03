<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-enable-debug-mode-in-a-metadefender-core-kubernetes-deplo -->

# How to Enable Debug Mode in a MetaDefender Core Kubernetes Deployment?

This article is applied to MetaDefender Core releases deployed on Linux systems in a Kubernetes container environment.

**Overview**

This article explains how to enable debug mode in a MetaDefender Core deployment running in a Kubernetes environment. Enabling debug mode increases the verbosity of log output, which can be helpful for troubleshooting and diagnostics. This setting should only be used when actively investigating issues, as it can produce large volumes of logs.

**Steps to Configure Debug Mode**

1. **Add the Debug Logging Environment Variable**: Modify your Kubernetes deployment to include the following environment variable in the container specification:

CORE_CONF_JSON: {"logger/loglevel":"debug"}

This variable instructs MetaDefender Core to set the logger level to 'debug' by injecting a JSON configuration at container startup.

**Example Snippet in Deployment YAML:**

Insert the following under the `env`: section of your container in the deployment manifest:

YamlCopyenv:
CORE_CONF_JSON: '{"logger/loglevel":"debug"}'

In an AWS Kubernetes deployment the variable can be set as below:

2. **Apply the Updated Deployment:**

After saving your modified deployment YAML, apply it using the following command:

`kubectl apply -f <your-deployment-file>.yaml`

This will restart the pod with the updated environment variable. If the variable was added in the POD creation, there is no need for an apply as shown above.

3. **Verify Debug Logging:**

Once the pod is running, you can check if debug mode is enabled by inspecting the logs:

`kubectl logs <pod-name> -n <namespace>`

Look for log entries that contain [`DEBUG`]. These confirm that the log level has been successfully elevated to debug.

4. **Revert to Standard Logging:**

Once debugging is complete, it is recommended to revert the log level to 'info' by changing the environment variable value to:

`CORE_CONF_JSON: {"logger/loglevel":"info"}`

**Troubleshooting Notes**

- Use debug mode temporarily, as it can increase log volume significantly. - Always monitor disk usage if debug logging is left enabled for extended periods.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

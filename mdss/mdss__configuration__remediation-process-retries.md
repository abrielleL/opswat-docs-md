<!-- source: https://www.opswat.com/docs/mdss/configuration/remediation-process-retries -->

# Remediation Process Retries

The remediation process includes automatic retry functionality to handle transient failures. When processing each file, the system will attempt up to **3 retries** if the initial remediation attempt fails. There is a **30-second interval** between each retry attempt to allow for temporary issues to resolve.

The retry interval is configurable through the `POLLY_POST_ACTION_RETRY_TIME` environment variable, allowing you to adjust the timing based on your specific requirements and infrastructure constraints.

### [Configuration Example](/docs/mdss/configuration/remediation-process-retries#configuration-example)

To extend the retry interval to 60 seconds, add the following to your `customer.env` file (instructions [here](/docs/mdss/configuration/custom-configuration)):

BashCopyPOLLY_POST_ACTION_RETRY_TIME=60

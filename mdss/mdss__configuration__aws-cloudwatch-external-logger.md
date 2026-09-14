<!-- source: https://www.opswat.com/docs/mdss/configuration/aws-cloudwatch-external-logger -->

# AWS CloudWatch External Logger

To use the AWS CloudWatch logging service, the following conditions must be met:

- AWS SSM agent installed, up to date and active on the EC2 instance (more info [here](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html))
- These IAM permissions allocated to the instance

  - AmazonSSMManagedInstanceCore
  - CloudWatchAgentServerPolicy
- AWS CloudWatch agent installed, up to date and active on the EC2 instance (more info [here](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html))

If the above conditions are met, the CloudWatch agent can be configured either through [editing its configuration file](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch-Agent-Configuration-File-Details.html) or from the [EC2 web UI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-and-configure-cloudwatch-agent-using-ec2-console.html) for your instance.

When configuring the log collection section, you can set specific paths and filenames or, alternatively, you can use wildcard characters (*) to cover multiple folders and/or files. If you want to collect logs from exact paths or specific files, one separate entry needs to be created for each folder or file.

You also have the option to group logs from multiple locations into one or several log groups and streams which will then be visible in AWS CloudWatch. A log group can contain one or multiple log streams, and each log stream can be set to collect logs from one or multiple log files.

Info

If you group logs from multiple files into the same log stream they will be combined and displayed in chronological order, there will be no separation based on the source log files.

An example configuration to collect CPU, RAM and disk storage metrics from a Linux installation every 5 seconds as well as to pull all MetaDefender Storage Security logs using wildcards would look like this:

Note

The example below will collect **all logs** from MetaDefender Storage Security.

If you would like to customize which logs are collected, please configure the paths according to the documented locations [here](/docs/mdss/where-to-get-help/log-location).

JsonCopy{
"agent": {
"metrics_collection_interval": 60
},
"metrics": {
"namespace": "CWAgent",
"append_dimensions": {
"InstanceId": "${aws:InstanceId}"
},
"metrics_collected": {
"mem": {
"measurement": [
"used_percent"
]
},
"cpu": {
"measurement": [
"usage_active"
]
},
"disk": {
"measurement": [
"used_percent"
]
}
}
},
"logs": {
"logs_collected": {
"files": {
"collect_list": [
{
"file_path": "/var/log/mdss/*.log",
"filters": [],
"log_group_name": "mdss-logs",
"log_stream_name": "applogs"
},
{
"file_path": "/etc/mdss/services_logs/*/*.txt",
"filters": [],
"log_group_name": "mdss-logs",
"log_stream_name": "applogs"
}
]
}
},
"log_stream_name": "mdss-logging"
}
}

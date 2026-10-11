<!-- source: https://www.opswat.com/docs/mdss/4.5.2/where-to-get-help/how-to-enable-extra-logging-in-the-configuration -->

# How to Enable Extra Logging in the Configuration?

Logging supports different log levels to have the desired granularity. Default logging is set to **Information**.

To change log level adjust **MinimumLevel.Default** as follows:

- Debug: provides detailed information useful for troubleshooting.
- Information: the default logging level, capturing general operational messages.
- Warning: only highlights potentially harmful situations.
- Error: logs only issues that affect functionality or cause interruptions.
- Fatal: reserved for very critical issues that require immediate attention.

A typical `appsettings.json` configuration file appears as follows depends on the desired Serilog Sink:

- for **File Serilog Sink**

> **Info**
>
> Default maximum size of a log file is 500Mb which can be adjust by changing `fileSizeLimitBytes`
>
> Rolling interval is configured to be daily by the `rollingInterval`or on file size limit `rollOnFileSizeLimit: true`
>
> Default limit of retained files is set to 10 using the `retainedFileCountLimit` property

```json
{
  "Serilog": {
    "Using": [],
    "MinimumLevel": {
      "Default": "Information",
      "Override": {
        "Microsoft": "Warning",
        "System": "Warning",
        "Microsoft.Hosting.Lifetime": "Warning"
      }
    },
    "Enrich": [ "FromLogContext", "WithMachineName", "WithProcessId", "WithProcessName", "WithThreadId" ],
    "WriteTo": [
      {
        "Name": "File",
        "Args": {
          "buffered": false,
          "fileSizeLimitBytes": 500000000,
          "outputTemplate": "[{Timestamp:u}] [{Level}] {Namespace}: {Message:lj}{NewLine}{Exception}",
          "path": "logs/log.txt",
          "retainedFileCountLimit": "10",
          "rollingInterval": "Day",
          "rollOnFileSizeLimit": true
        }
      }
    ]
  }
}
```

- for **HTTP Serilog Sink**

```json
{
  "Serilog": {
    "MinimumLevel": {
      "Default": "Information",
      "Override": {
        "Microsoft": "Warning",
        "System": "Warning",
        "Microsoft.Hosting.Lifetime": "Information"
      }
    },
    "Enrich": [
      "FromLogContext",
      "WithMachineName",
      "WithProcessId",
      "WithProcessName",
      "WithThreadId"
    ],
    "WriteTo": [
      {
        "Name": "Http",
        "Args": {
          "requestUri": "<REQUEST_URI>",
          "queueLimitBytes": null
        }
      }
    ]
  }
}
```

- for **Syslog Serilog Sink**

```json
{
  "Serilog": {
    "Using": [
      "Serilog.Sinks.Syslog"
    ],
    "MinimumLevel": {
      "Default": "Information",
      "Override": {
        "Microsoft": "Warning",
        "System": "Warning",
        "Microsoft.Hosting.Lifetime": "Information"
      }
    },
    "Enrich": [
      "FromLogContext",
      "WithMachineName",
      "WithProcessId",
      "WithProcessName",
      "WithThreadId"
    ],
    "WriteTo": [
      {
        "Name": "TcpSyslog",
        "Args": {
          "host": "<HOST>",
          "port": 514,
          "appName": "MetaDefenderStorageSecurity",
          "format": "RFC5424",
          "facility": "<SYSLOG_FACILITY_NAME>",
          "outputTemplate": "[{Timestamp:u}] [{Level}] {SourceContext}: {Message:lj}{NewLine}{Exception}"
        }
      }
    ]
  }
}
```

## Linux-based systems

Use the **appsettings.json**  file from the `configurations` directory

**Note:** The default path on Linux is`/etc/mdss/configurations`.

> On Linux, logging settings are applied immediately after any changes, so a system restart is not required.

## Windows-based systems

On Windows systems, each service has its own logging configuration file. You can locate the `appsettings.json` file by navigating to the service's directory and then accessing the specific `<service>` folder.

**Note**: The default path on Windows is `C:\Program Files\OPSWAT\MetaDefender Storage Security\services\`.

> On Windows, logging settings take effect only after the service has been restarted.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

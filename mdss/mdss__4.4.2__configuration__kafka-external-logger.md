<!-- source: https://www.opswat.com/docs/mdss/4.4.2/configuration/kafka-external-logger -->

# Kafka External Logger

For adding a new Kafka external logger configuration, you will need to enter the following details on the **Add External Logger Configuration window:**

- **Integration type**: Select **Kafka**
- **Server addresses with ports** - Ipv4, Ipv6 and Host Name formats are supported with the port specified for each of them (multiple addresses can be separated with a comma)
- **Topic**: The Kafka topic where the logs will be sent
- **Security Protocol**: Select the desired protocol from Plaintext, SASL Plaintext, SASL SSL or SSL

For SASL Plaintext and SASL SSL security protocols, the following fields are also required:

- **SASL mechanism**: Select the desired mechanism from Plain, SCRAM SHA 256 and SCRAM SHA 512
- **SASL username**: The SASL username
- **SASL password**: The SASL password

## [Kafka message format:](/docs/mdss/4.4.2/configuration/kafka-external-logger#kafka-message-format)

The log messages sent are sent as JSON, and contain information such as the timestamp, log type, level and the log message.

Message sampleCopy{
"Timestamp": "2024-11-18T09:13:43.4018931+00:00",
"Level": "Information",
"MessageTemplate": "{User} logged in.",
"RenderedMessage": "\"User (John Doe)\" logged in.",
"Properties": {
"User": "User(John Doe)",
"Namespace": "ExternalLogger",
"EventTimestamp": "2024-11-18 09:13:43",
"UserName": "User",
"UserId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx",
"Category": 3,
"LogType": 600
}
}
## [Logging non-audit MDSS messages to Kafka:](/docs/mdss/4.4.2/configuration/kafka-external-logger#logging-non-audit-mdss-messages-to-kafka)

For logging other log messages produced by MDSS the appsettings.json can be modified to include a configuration to write to Kafka such as:

JsonCopy{
"Serilog": {
"MinimumLevel": {
"Default": "Information",
"Override": {
"Microsoft": "Warning",
"System": "Warning",
"Microsoft.Hosting.Lifetime": "Information"
}
},
"Enrich": [ "FromLogContext", "WithMachineName", "WithProcessId", "WithProcessName", "WithThreadId" ],
"WriteTo": [
{
"Name": "Kafka",
"Args": {
"bootstrapServers": "kafkaServerAddress1:kafkaport1,kafkaServerAddress2:kafkaport2",
"securityProtocol": "Plaintext",
"topic": "mdss",
"messageKey": "EventTimestamp"
}
}
]
}
}

For "**securityProtocol"** values can be Plaintext, SaslSsl, SaslPlaintext or Ssl. For using SASL, the "**saslMechanism"** can be specified with values such as Plain, ScramSha512 or ScramSha256. For example, to use SASL with a Plain mechanism with username and password, the following values can be added to the Args key in the appsettings Kafka configuration.

JsonCopy{
"saslMechanism": "Plain",
"saslUsername": "username",
"saslPassword": "password",
}

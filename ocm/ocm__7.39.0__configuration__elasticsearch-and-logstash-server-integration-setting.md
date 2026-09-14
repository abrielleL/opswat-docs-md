<!-- source: https://www.opswat.com/docs/ocm/7.39.0/configuration/elasticsearch-and-logstash-server-integration-setting -->

# Elasticsearch and Logstash server integration settings

OPSWAT Central Management supports integration with Elasticsearch and Logstash technology stack for enhanced product management capability.

Elasticsearch is a distributed, free and open search and analytics engine for all types of data, including textual, numerical, geospatial, structured, and unstructured. Logstash is an open-source data collection engine with real-time pipelining capabilities and can dynamically unify data from disparate sources (such as managed MetaDefender Core and MetaDefender Kiosk instances) and normalize the data into an Elasticsearch server. Through the two features [MetaDefender Core dashboard](/docs/ocm/7.39.0/integrations/metadefender-core) and [MetaDefender Kiosk dashboard](/docs/ocm/7.39.0/integrations/metadefender-kiosk), OPSWAT Central Management visualizes the data stashed in the Elasticsearch server in a more readable and user-friendly format.

From version 7.14, OPSWAT Central Management can also send logs related to the device management feature (integrated MetaDefender IT-OT Access module) to the Logstash server for safekeeping.

For more information on [Elasticsearch](https://www.elastic.co/elasticsearch/) and [Logstash](https://www.elastic.co/logstash), please refer to the corresponding links.

Warning

Please note that OPSWAT Central Management is currently only compatible with the 7.x versions of Elasticsearch and Logstash.

The below guidelines describes how to configure existing Elasticsearch and Logstash servers to use with OPSWAT Central Management.

1. Install and set up the Elasticsearch server. For more details on how to install an Elasticsearch server, please [visit the official Elastic website](https://www.elastic.co/downloads/elasticsearch).

**(Optional)** OPSWAT Central Management provides an example configuration file elasticsearch.yml that can be copied to the Elasticsearch installation's config folder to set up the server. Please accept the file overwrite request if you choose to use the example configuration.

- On Windows, the file is located at C:\Program Files\OPSWAT\Central\elk-config\elasticsearch\config\elasticsearch.yml

- On Red Hat 7, the file is is located at /opt/ocm/elk-config/elasticsearch/config/elasticsearch.yml

2. Locate the address that the Elasticsearch server is listening on. This address corresponds to the items **network.host** and **http.port** in the configuration file elasticsearch.yml For example:

   - **network.host: 0.0.0.0** indicates that the Elasticsearch server binds to all network interfaces on the system This means that the Elasticsearch server can be connected to via any network interfaces present on the system, e.g., via the **localhost** hostname through the loopback network interface.
   - **http.port: 9200** indicates that the Elasticsearch server binds to port 9200.
3. Install and set up the Logstash server. For more details on how to install a Logstash server, please visit [the official Elastic website](https://www.elastic.co/downloads/logstash).

**(Optional)** OPSWAT Central Management provides an example configuration file logstash.yml that can be copied to the Logstash installation's config folder to set up the server. Please accept the file overwrite request if you choose to use the example configuration.

- On Windows, the file is located at C:\Program Files\OPSWAT\Central\elk-config\logstash\config\logstash.yml

- On Red Hat 7, the file is is located at /opt/ocm/elk-config/logstash/config/logstash.yml

4. Locate the Logstash pipeline configuration file logstash_ocm.conf included in the OPSWAT Central Management's installation folder, which contains important settings used for OPSWAT Central Management's integration.

   - On Windows, the file is located at C:\Program Files\OPSWAT\Central\elk-config\logstash\config\logstash_ocm.conf
   - On Red Hat 7, the file is is located at /opt/ocm/elk-config/logstash/config/logstash_ocm.conf
5. Copy logstash_ocm.conf to the Logstash's config folder.
6. Modify logstash_ocm.conf with the correct parameters of the Elasticsearch and Logstash servers. The following settings should be considered for modifications:

   - **port => 9020** is the port bound by the Logstash server to listen for syslog sent from OPSWAT Product instances via the corresponding protocol, such as UDP or TCP.
   - **hosts => "localhost:9200"** is the address of the Elasticsearch server that the Logstash server should connect to. The default address **localhost:9200** assumes that both Elasticsearch and Logstash are installed on the same system and that the Elasticsearch server is listening on port 9200. Please review step 2 to locate the address of your Elasticsearch server.

An example of the aforementioned configuration in logstash_ocm.conf:

input {
tcp {
port => 9020
type => syslog
}
udp {
port => 9020
type => syslog
}
}
#Integration setting for OPSWAT Central Management is placed here in the actual file
#Please do not modify
output {
if [type] == "syslog" and "_grokparsefailure" in [tags] {
file { path => "logs/failed_syslog_events-%{+YYYY-MM-dd}" }
}
if [sessionID] {
elasticsearch {
hosts => "localhost:9200"
document_id => "%{[cm_session_index]}" #Integration setting, please do not modify
}
} else {
elasticsearch {
hosts => "localhost:9200"
}
}

7. Start the Elasticsearch server. For example, on Windows, via a command-line interface:

cd <Elasticsearch's installation folder>
bin\elasticsearch.bat

Please refer to [the official Elasticsearch documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/starting-elasticsearch.html) for how to start the Elasticsearch server on your system. The aforementioned documentation should also include instructions to set up the Elasticsearch server as a service to allow automatic startup.

8. Start the Logstash server with the logstash_ocm.conf configuration file. For example, on Windows, via a command-line interface:

cd <Logstash's installation folder>
bin\logstash.bat -f config\logstash_ocm.conf

Please refer to [the official Logstash documentation](https://www.elastic.co/guide/en/logstash/current/setup-logstash.html) for how to start the Logstash server on your system. The aforementioned documentation should also include instructions to set up the Logstash server as a service to allow automatic startup.

9. In the OPSWAT Central Management console, navigate to **Settings > Server Configuration > ELK** to configure settings related to Elasticsearch and Logstash, .

- **Address, Port (required fields)**: The addresses of the Elasticsearch and Logstash servers. Please review step 6 to determine the correct addresses.

- **Elasticsearch only:**

- **(Optional) Username, Password**: The credentials used to access the Elasticsearch server if present. OPSWAT Central Management currently only supports the Basic authentication scheme

- **Logstash only:**

- **Protocol**: The protocol used to connect to the Logstash server (UDP or TCP).

- **(Optional) Aggregate OPSWAT Central Management logs to Logstash (UDP only):** Allows OPSWAT Central Management to also send device management logs to the Logstash server. This option is only available for the UDP protocol.

- **Test Connection**: Test the connection to both Elasticsearch and Logstash servers. To succeed, the Logstash server should already be connected to the Elasticsearch server.

Warning

OPSWAT Central Management currently does not support pushing ELK configuration to MetaDefender Core instances. Please refer to [MetaDefender Core documentation](https://onlinehelp.opswat.com/corev4/3.2.1.__Startup_Core_Configuration.html) for more details on how to configure its ELK settings.

Info

On adding a new MetaDefender Kiosk instance to OPSWAT Central Management, the Logstash server configuration will be pushed to this instance. Please refer to [Adding an existing MetaDefender Kiosk Windows instance](/docs/ocm/7.39.0/integrations/adding-an-existing-metadefender-kiosk-instance) for more details on how to add an existing MetaDefender Kiosk instance.

Info

After the Elasticsearch and Logstash servers are successfully configured and at least one MetaDefender Kiosk instance is connected with correct Logstash server configuration, [MetaDefender Kiosk dashboard](/docs/ocm/7.39.0/integrations/metadefender-kiosk) will be displayed properly.

Warning

OPSWAT Central Management does not push Logstash configuration retroactively to MetaDefender Kiosk instances before the Logstash configuration was created. Any such instances must be manually configured. OPSWAT Central Management also does not re-push Logstash configuration on modification. All MetaDefender Kiosk instances under management will require manual configuration. Please refer to [Changing MetaDefender Kiosk Windows Configuration](/docs/ocm/7.39.0/integrations/changing-metadefender-kiosk-configuration) for more detail on how to manually configure a MetaDefender Kiosk instance.

#### [Syslog message format](/docs/ocm/7.39.0/configuration/elasticsearch-and-logstash-server-integration-setting#syslog-message-format)

Because OPSWAT Central Management's syslog is originally implemented according to other OPSWAT Products' integration, please refer to their respective documentation

- [MetaDefender Core](https://docs.opswat.com/mdcore/configuration/syslog-message-format)
- [MetaDefender Kiosk](https://docs.opswat.com/mdkiosk/advanced-deployment/syslog-settings#syslog-message-format)
- [Device management feature (integrated MetaDefender IT-OT Access module)](https://docs.opswat.com/macloud-sdp/configuration---management/siem-integration#syslog)

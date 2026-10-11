<!-- source: https://www.opswat.com/docs/filescan/3.2.0/troubleshooting/services-and-system-components -->

# Services and System Components

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Sandbox Service](/docs/filescan/3.2.0/troubleshooting/services-and-system-components#sandbox-service)

The Sandbox service consists of several Docker containers that implement different components of the system.

Internally, `docker compose` is used to manage all containers and networks in Docker.

The `sudo docker ps` command can be used to check the status of these containers. This is how the list of containers should look typically:

It is important to check if the following critical containers are listed and healthy:

- webservice
- nginx/reverse_proxy
- redis
- mongodb
- arangodb/graphdb
- broker
- transform

The logs for each container can be displayed in real time, e.g.:

BashCopydocker logs -f broker

The following helper scripts should be used to start/stop the `sandbox` service (including all containers):

BashCopy/home/sandbox/sandbox/stop_sandbox.sh
/home/sandbox/sandbox/start_sandbox.sh

It is also possible to interact with the `sandbox` service as a system service (this will produce very little output):

BashCopysudo service sandbox stop
sudo service sandbox start

Additional commands are available to restart all components, or the broker and transform selectively:

BashCopysudo service sandbox restart
sudo service sandbox restart-broker
sudo service sandbox restart-transform
## [Database storage location](/docs/filescan/3.2.0/troubleshooting/services-and-system-components#database-storage-location)

The MongoDB (db) and ArangoDB (graphdb) database files are stored in the `/data` directory:

---

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

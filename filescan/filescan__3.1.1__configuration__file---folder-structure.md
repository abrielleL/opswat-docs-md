<!-- source: https://www.opswat.com/docs/filescan/3.1.1/configuration/file---folder-structure -->

# File / Folder Structure

Sandbox will be installed in the `/home/sandbox/sandbox` directory by default.

If the default options are used, the following top-level folders will be created:

- **logs**: Contains logfiles collected from various components, see: [Logging](/docs/filescan/3.1.1/troubleshooting/logging)
- **broker**: Contains the "broker" component
- **transform**: Contains the "transform" analyzer engine
- **webservice**: Contains the Sandbox webservice that implements the top-level Sandbox API
- **webservice-front**: Contains the Sandbox frontend
- **THIRD-PARTY**: Contains license information from open-source libraries

The descriptions of potentially relevant folders in `/home/sandbox/sandbox/transform` are provided for informational purposes only:

- **consumers**: This is where a group of Python scripts reside, which can consume reporting data and generate informational signals of different severity levels. These "signals" are often referred to as behavior indicators / signatures by different security vendors. The term "signal" is used to underline the fact that a lot of reporting contains much "noise" (redundant information) of which the relevant signals need to be extracted.
- **external**: This folder has a variety of definitions (e.g. a list of UUIDs, MITRE techniques/tactics or local whitelists/blacklists). These files are actively maintained, and new versions are provided with each update.
- **lib**: This folder contains a variety of third-party libraries that are used by the processor node. Do not modify this folder.
- **parser**: This folder contains a variety of external scripts / integrations that are used by the processor node. Do not modify this folder.
- **thirdparty**: This folder contains a variety of third-party software not relevant to the core functionality. Do not modify this folder.
- **yara**: This folder contains a variety of third party and local YARA rules, which are compiled to a master index file and used against the input file and extracted artifacts. In general, do not modify this folder, although it is possible to add custom [YARA Rules](/docs/filescan/3.1.1/configuration/yara-rules) here.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

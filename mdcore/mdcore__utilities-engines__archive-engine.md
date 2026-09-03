<!-- source: https://www.opswat.com/docs/mdcore/utilities-engines/archive-engine -->

# Archive Extraction Engine

Detecting threats in compressed files, such as .ZIP or .RAR, can be difficult due to their large file size and ability to mask hidden threats such as archive bombs (malicious files designed to crash anti-malware programs). MetaDefender offers fast processing of archives by allowing administrators to perform archive handling once for each file type, instead of requiring each individual anti-malware engine to use its own archive handling methods. Additionally, administrators can customize the way archive scanning is performed to avoid threats like zip bombs.

### [System requirement](/docs/mdcore/utilities-engines/archive-engine#system-requirement)

- On Linux: To extract password protected MS Office files, you need to install [.NET 8 dependencies](https://docs.opswat.com/mdcore/knowledge-base/how-to-install-net-6-runtime-dependencies-on-Linux-Distribu)

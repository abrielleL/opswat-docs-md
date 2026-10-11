<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/utilities-engines/yara-engine -->

# YARA Engine

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### [Rule sources](/docs/mdcore/v5.22.1/utilities-engines/yara-engine#rule-sources)

Under **Inventory/Modules** menu it is possible to configure custom **YARA sources.**

To add new source, click on **Add new source** button. You can specify the type of the source, and the URL itself. The product supports 2 types of YARA sources: local directory and network source (HTTP/HTTPS). A network source must be a zip file. The content of the zip file will be used by the YARA engine. As a local directory, you can set a local path on the computer. This path must point to a directory. A copy of this directory will be used by the YARA engine.

To generate a package, click on the **Generate package** button. This will start the process, and the start time will be shown next to the buttons. Next to the sources, you can enable or disable the sources. Disabled sources will not be used when generating the next package.

Sources can be modified by clicking the row and removed by clicking the trash icon on the right side of the rows.

Please note that the included YARA modules are the following:

- [Magic](https://yara.readthedocs.io/en/v3.8.1/modules/magic.html)
- [Hash](https://yara.readthedocs.io/en/v3.8.1/modules/hash.html)
- [Dotnet](https://yara.readthedocs.io/en/v3.8.1/modules/dotnet.html)
- Macho
- Dex
- [Cuckoo](https://yara.readthedocs.io/en/v3.8.1/modules/cuckoo.html)
- [Androguard](https://docs.koodous.com/yara/androguard/)

For more details, check [YARA modules documentation](https://yara.readthedocs.io/en/v3.8.1/modules.html).

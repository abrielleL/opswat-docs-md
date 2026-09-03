<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/metascan-engines/configure-clamav-to-use-a-custom-database -->

# Configure ClamAV to use a custom database

ClamAV allows you to create your own database to improve the detection, please see [this page](https://docs.clamav.net/manual/Signatures.html#creating-signatures-for-clamav) to lean more about how to create a custom database.

To use the custom database in MetaDefender Core:

- go to Inventory > Modules > Metascan > ClamAV
- Enable Custom Database, set Custom Database Path to the custom database folder

After saving the configuration, you can verify if the Metascan Core uses the new file or not by checking the ClamAV folder in **<MetaDefender Core installation folder>\data\engines\clamav_********_**\database**, if there is an file started with **EXT_** which means the configuration was set successfully.

A simple test to validate this feature

- Create a text file with this format: <**md5>**:<**file size>**:<**malware name>,** for example**:** 385141700748a2cfa2d746fb8899efe6:35:My_Malware_Name**,** save it with **.hdb** extension to a folder
- Set the ClamAV custom database path to that folder
- Scan the file which has the same MD5 in text file, ClamAV should detect the file as infected with "<malware name>.UNOFFICIAL" as a threat name

### [Custom Database Example](/docs/mdcore/v5.21.0/metascan-engines/configure-clamav-to-use-a-custom-database#custom-database-example)

Disclaimer

This information is provided for general informational purposes only. OPSWAT is not responsible for the accuracy or reliability of any information provided. The examples mentioned are for illustration only and do not constitute an endorsement by OPSWAT.

- SecuriteInfo [<https://www.securiteinfo.com>]
- Sanesecurity [<https://sanesecurity.com/>]
- URLhaus [<https://urlhaus.abuse.ch/api/#clamav>]
- PhishTank [<https://phishtank.com/>]
- Interserver [<https://www.interserver.net/>]
- Linux Malware Detect [<https://www.rfxn.com/projects/linux-malware-detect/>]
- OpenPhish [<https://openphish.com/>]

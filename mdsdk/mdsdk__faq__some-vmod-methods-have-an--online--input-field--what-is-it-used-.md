<!-- source: https://www.opswat.com/docs/mdsdk/faq/some-vmod-methods-have-an--online--input-field--what-is-it-used- -->

# Some vmod methods have an "online" input field. What is it used for?

There are currently five methods that include the "online" input field: GetLatestInstaller(50300), InstallFromFiles(50301), GetProductPatchLevel(50500), IsDefunct(50502), GetRemediations(50503), and GetProductVulnerability(50505).

When you set the "online" input field to 1, these methods will use the online database specified during `wa_api_setup` with the "online_database_uri" input field, instead of the offline database loaded by LoadPatchDatabase(50302) or ConsumeOfflineVmodDatabase(50520).

Opswat publishes the cloud database under the name `full_db.zip`. Its contents should be mirrored properly on a CDN and be accessible via the URI specified by the "online_database_uri" input field in the `wa_api_setup` call. New files can be added, and existing files can be deleted or modified. Currently, online mode supports patching for third-party products using only the GetLatestInstaller and InstallFromFiles methods.

Example of how to use online mode:

TextCopyAt client side:
1. Need to set WA_VMOD_CONFIG_ONLINE_DATABASE_URI when calling wa_api_setup method.
Ex:{... "online_database_uri" : "https://cdn.yourdomain/cloud_db/" ...}
2. Need to set "online" as 1 when calling GetLatestInstaller or InstallFromFiles method.
Ex:{... "online" : 1 ...}
On server/CDN servers:
1. Need to deploy files and folders extracted from the attached file to the HTTP/HTTPS location set above.
Ex:
https://cdn.yourdomain/cloud_db/
|_defunct
|_feed
|_patch
|_rem
|_vuln
|_header.json

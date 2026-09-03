<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-do-i-reset-all-skip-by-hash-entries-in-metadefender-core- -->

# How do I reset all Skip by Hash Entries in MetaDefender Core?

**Check Your Version:** This article applies to MetaDefender Core and is applicable to all MetaDefender Core V5 releases deployed on Windows and Linux systems.

Warning

Please note that this process will delete all stored entries in the Skip by Hash lists. These lists are global and take precedence during file scans. After the deletion, workflow settings will assume priority.

> Overview

When multiple skip-by-hash entries are present, or the volume is too large to manage manually, this method provides the recommended approach of using an API call to efficiently clear the list. Screenshot of a populated Skip by Hash list.

## [Steps to Configure](/docs/mdcore/knowledge-base/how-do-i-reset-all-skip-by-hash-entries-in-metadefender-core-#steps-to-configure)

The command syntax depends on the operating system where MetaDefender Core is installed.

### [For Windows (Command Prompt):](/docs/mdcore/knowledge-base/how-do-i-reset-all-skip-by-hash-entries-in-metadefender-core-#for-windows-command-prompt)

curl --request PUT ^
--url "http://YOUR CORE IP HERE:8008/admin/config/skip" ^
--header "Content-Type: application/json" ^
--header "apikey: YOUR API KEY HERE" ^
--data "{ \"blacklist\": {}, \"skip\": {}, \"whitelist\": {} }"
### [For Linux/macOS (Shell / Bash):](/docs/mdcore/knowledge-base/how-do-i-reset-all-skip-by-hash-entries-in-metadefender-core-#for-linuxmacos-shell--bash)

curl --request PUT \
--url 'http://YOUR CORE IP HERE:8008/admin/config/skip' \
--header 'Content-Type: application/json' \
--header 'apikey: YOUR API KEY HERE' \
--data '{
"blacklist": {},
"skip": {},
"whitelist": {}}'

Screenshot of what the API call would look like on the Linux system.

After executing the curl command, the shell output returned a JSON-formatted API response.

## [Verify the Change](/docs/mdcore/knowledge-base/how-do-i-reset-all-skip-by-hash-entries-in-metadefender-core-#verify-the-change)

After running the API call, verify that all skip by hash lists are cleared.

Screenshot of a cleared Skip by Hash list which shows that the API call has successfully removed all Skip by Hash entries.

Support

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).

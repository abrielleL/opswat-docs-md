<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-am-i-getting-a--file-not-found--invalid-path-or-access--erro -->

# Why am I getting a "File not found, invalid path or access" error when using the 'filepath' header in the RestAPI on Linux?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to MetaDefender Core All MetaDefender Core releases deployed on Linux.

When using the RestAPI to send a file under the header ‘filepath', the error 'File not found, invalid path or access’ is returned.

# curl -X POST http://MDCORE-HOST:8008/file -H "apikey: xxxxxxxxxxxxxx" -H "filepath:/home/admin/test.txt" -H "rule:xxxxx"
{"err":"File not found, invalid path or access."}

Even though the file exists and is accessible when traversed manually.

# ls -la /home/admin/test.txt
-rwxrwxrwx. 1 root root 5 Nov 12 09:39 /home/admin/test.txt
# namei -l /home/admin/test.txt
f: /home/admin/test.txt
dr-xr-xr-x root root /
drwxr-xr-x root root home
drwxr-x--- admin admin admin
-rwxrwxrwx root root test.txt

**Main Cause:**

MetaDefender Core runs as the ‘metascan' user. When a request is made with the ‘filepath’ header, the 'metascan’ user requires explicit permission to access the file, beyond the permissions granted to normal or root users.

# sudo -u metascan namei -l /home/admin/test.txt
f: /home/admin/test.txt
dr-xr-xr-x root root /
drwxr-xr-x root root home
drwxr-x--- admin admin admin
test.txt - Permission denied

**Resolution:**

The `metascan` user needs at least 'Execute' (x) permission at each folder/file level to access the file. Adjust the permissions on the directory level to grant 'execute' permission. For example:

# chmod +x /home/admin/
# sudo -u metascan namei -l /home/admin/test.txt
f: /home/admin/test.txt
dr-xr-xr-x root root /
drwxr-xr-x root root home
drwxr-x--x admin admin admin
-rwxrwxrwx root root test.txt

Then, verify again

# curl -X POST http://MDCORE-HOST:8008/file -H "apikey: xxxxxxxxxxxxxx" -H "filepath:/home/admin/test.txt" -H "rule:xxxxx"
{"data_id":"95690812c3594522a18ce2b3c8a2ae7b"}Support:

If Further Assistance is required, please proceed to [log a support case or chatting with our support engineer](https://my.opswat.com/support).

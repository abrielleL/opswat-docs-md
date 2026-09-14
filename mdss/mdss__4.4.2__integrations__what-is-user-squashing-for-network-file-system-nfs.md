<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/what-is-user-squashing-for-network-file-system-nfs -->

# What is User Squashing for Network File System (NFS)

In NFS (Network File System), **user squashing** is a security mechanism that controls how user IDs (UIDs) are mapped between the client and server machines. It helps protect the server from potential security risks when users connect with elevated privileges.

Here's a breakdown of different concepts, containing an example of how the `/etc/exports` file look like:

**1. Root Squashing:**

- By default, root squashing is enabled. This means when a user with root privileges (UID 0) on the client attempts to access the NFS share, their UID is mapped to a specific user on the server, typically "nobody" (UID 65534). This user typically has limited permissions, preventing the client root user from performing actions that could compromise the server.

**2. All Squashing:**

- This option maps all client user IDs to a single user on the server, usually "nobody." This provides minimal permissions to all users accessing the share, regardless of their privileges on the client machine. Use this cautiously as it can severely limit functionality.

`/shared/data *(rw,sync,nfsvers=4,all_squash)`

- There is also the option to map all client user IDs to a specific user. You will need to create the dedicated user, set permissions and assign it to a group. Here is an example of how`/etc/exports` file looks

`/path/to/shared/folder *(rw,sync,root_`*squash,user*`mapping=(to="dedicated_user", squash))`

**3. No_root_squash:**

- This option disables user squashing altogether. It allows client users, including root, to retain their original UIDs on the server. This can be risky as it grants potentially harmful permissions to users, especially root. Only use this in trusted environments and with explicit security measures.

`/shared/data *(rw,sync,nfsvers=4,no_root_squash)`

You can find more details on the official documentation of the NFS protocol: <https://docs.kernel.org/admin-guide/nfs/index.html>

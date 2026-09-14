<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/resolve-waapi-error-resource-busy-from-installmissingpatches -->

# Resolving WAAPI_ERROR_RESOURCE_BUSY error from InstallMissingPatches method

### [Problem](/docs/mdsdk/knowledge-base/resolve-waapi-error-resource-busy-from-installmissingpatches#problem)

This issue is commonly observed on Debian-based Linux distributions, especially Ubuntu, where the `InstallMissingPatches` method may return the error `WAAPI_ERROR_RESOURCE_BUSY`. This error prevents the installation process from proceeding during the method's invocation.

The root cause is OS-level locking of the package management system, which can cause `InstallMissingPatches` to be delayed or hang. For instance, the APT package manager may return this error if another process is already using it (e.g., `unattended-upgrade`, `aptd`, etc.).

Here is an example of what may delay `InstallMissingPatches`:

### [Solution](/docs/mdsdk/knowledge-base/resolve-waapi-error-resource-busy-from-installmissingpatches#solution)

#### [Option 1: Wait until the locking process is released](/docs/mdsdk/knowledge-base/resolve-waapi-error-resource-busy-from-installmissingpatches#option-1-wait-until-the-locking-process-is-released)

You can check for processes that may be preventing the system from installing packages using the following command:

sudo fuser /var/lib/dpkg/lock-frontend

or

sudo fuser /var/lib/dpkg/lock

The returned PIDs are the processes that lock the `dpkg` package installation.

#### [Option 2: Find the process frontend and quit it](/docs/mdsdk/knowledge-base/resolve-waapi-error-resource-busy-from-installmissingpatches#option-2-find-the-process-frontend-and-quit-it)

Please note that a crash report might appear when the frontend closes unexpectedly.

#### [Option 3: Terminate the processes holding the lock](/docs/mdsdk/knowledge-base/resolve-waapi-error-resource-busy-from-installmissingpatches#option-3-terminate-the-processes-holding-the-lock)

Warning

We should only terminate this process if there is no other option and we are forced to proceed.

**Step 1 – Identify lock-holding processes**

Check for any processes that are preventing package installation (e.g., those holding `apt / dpkg` locks).

**Step 2 – Terminate those processes gracefully**

1. Send `SIGTERM` (15) to each lock-holding process to let it stop, clean up, and exit.
2. If a process does not terminate after `SIGTERM`, send `SIGKILL` (9) to force it to exit.

kill <pid>

or

kill -15 <pid> # gracefil terminate

or

kill -9 <pid> # force kill

**Step 3 – Complete pending configurations**

Run:

dpkg --configure --pending

This finishes any unfinished package configurations, brings the system to a consistent state, and merges `dpkg` journal updates into the main status database.

**Step 4 – Verify locks are cleared**

Re-check for lock-holding processes. If none remain, `InstallMissingPatches` should execute normally.

#### [Option 4: Reboot the endpoint](/docs/mdsdk/knowledge-base/resolve-waapi-error-resource-busy-from-installmissingpatches#option-4-reboot-the-endpoint)

Warning

- Ensure all unsaved work is saved before restarting your system.
- Check whether there are any periodic jobs (e.g., via cron or systemd timers) that invoke dpkg or its frontends, and disable them temporarily. These jobs may trigger processes that lock the dpkg installation immediately after a reboot, causing conflicts.

This option will restart your operating system, terminate all remaining tasks, and help prevent the `WAAPI_ERROR_RESOURCE_BUSY` error from occurring during `InstallMissingPatches`.

### [Reference](/docs/mdsdk/knowledge-base/resolve-waapi-error-resource-busy-from-installmissingpatches#reference)

<https://wiki.debian.org/Teams/Dpkg/FAQ#Q:_What_can_be_done_when_the_dpkg_lock_is_held.3F>

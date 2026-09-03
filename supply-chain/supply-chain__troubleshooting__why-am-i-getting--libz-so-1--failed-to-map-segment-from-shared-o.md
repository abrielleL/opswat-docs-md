<!-- source: https://www.opswat.com/docs/supply-chain/troubleshooting/why-am-i-getting--libz-so-1--failed-to-map-segment-from-shared-o -->

# Why am I getting "libz.so.1: failed to map segment from shared object" error in Docker?

> **Check Your Version:**
>
> This article applies to all MetaDefender Software Supply Chain releases deployed on Linux systems.

**Issue:**

MetaDefender Software Supply Chain encountered an error when interacting with "docker-compose": `Error while loading shared libraries: libz.so.1: failed to map segment from shared object: Operation not permitted`

**Cause:**

If the /tmp mount is on restricted access and with `noexec` flag, it interferes with `docker-compose` requirement of `exec` mode for /tmp directory. More details [here](https://github.com/docker/compose/issues/8041) (external link to GitHub).

Double check if the /tmp mount currently has the `noexec` flag:

- `findmnt -l | grep tmp`

**Resolution:**

To resolve this issue, if the /tmp mount does have the `noexec` flag, perform the following steps:

1. Run the following command to re-mount the /tmp and give it execute permission:
   - `sudo mount /tmp -o remount,exec`
2. Restart the MetaDefender Software Supply Chain service: `sudo mdssc -c restart`

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).

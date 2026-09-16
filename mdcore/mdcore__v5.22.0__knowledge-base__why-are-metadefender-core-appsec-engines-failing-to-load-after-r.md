<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-are-metadefender-core-appsec-engines-failing-to-load-after-r -->

# Why are MetaDefender Core AppSec Engines Failing to Load After RHEL 8 to RHEL 9 Upgrade?

**Applies to**
MetaDefender Core 5.x on **RHEL 9** after in-place upgrade from **RHEL 8**, especially hardened builds where engine paths may inherit `noexec`.

## [**Summary**](/docs/mdcore/v5.22.0/knowledge-base/why-are-metadefender-core-appsec-engines-failing-to-load-after-r#summary)

Post-upgrade, some Core servers fail to start AppSec engines. The `engines` directory may be empty or engines fail self-tests with errors like:

- `Wait for hello message timeout`
- `failed to map segment from shared object`

**Primary cause:** the filesystem hosting engines is mounted with `noexec`. Contributing factors: missing RHEL 9 libraries and SELinux denials.

## [**Symptoms**](/docs/mdcore/v5.22.0/knowledge-base/why-are-metadefender-core-appsec-engines-failing-to-load-after-r#symptoms)

- Engines don’t load / self-tests fail.
- `engines` folder not repopulating after updates or manual copy.
- Errors as above in UI/logs.

## [**Diagnosis**](/docs/mdcore/v5.22.0/knowledge-base/why-are-metadefender-core-appsec-engines-failing-to-load-after-r#diagnosis)

1. **Mount options**

   ENGINES_DIR=/var/lib/ometascan/engines
   findmnt -T "$ENGINES_DIR"
   grep -nE ' /var |/ometascan|/engines' /etc/fstab

   If you see `noexec`, engines can’t run.
2. **SELinux status/denials**

   getenforce
   ausearch -m avc -ts recent | tail -n 50
3. **RHEL 9 deps present?**

   rpm -q libnsl krb5-libs libicu openssl-libs zlib compat-openssl11 || true

## [**Resolution**](/docs/mdcore/v5.22.0/knowledge-base/why-are-metadefender-core-appsec-engines-failing-to-load-after-r#resolution)

#### [**A. Remove** `noexec` **from engines filesystem**](/docs/mdcore/v5.22.0/knowledge-base/why-are-metadefender-core-appsec-engines-failing-to-load-after-r#a-remove-noexec-from-engines-filesystem)

- Edit `/etc/fstab` to drop `noexec` for the partition backing engines (e.g., `/var`).
- Remount:

  sudo mount -o remount,exec /var
  findmnt -T /var/lib/ometascan/engines

  *If policy requires* `noexec` *on* `/var`*, move engines to a dedicated* `exec` *mount and bind-mount back.*

#### [**B. Install required libraries**](/docs/mdcore/v5.22.0/knowledge-base/why-are-metadefender-core-appsec-engines-failing-to-load-after-r#b-install-required-libraries)

sudo dnf install -y libnsl krb5-libs libicu openssl-libs zlib compat-openssl11
#### [**C. Address SELinux (only if AVCs present)**](/docs/mdcore/v5.22.0/knowledge-base/why-are-metadefender-core-appsec-engines-failing-to-load-after-r#c-address-selinux-only-if-avcs-present)

- Temporary for troubleshooting:

  sudo setenforce 0 # revert with: sudo setenforce 1
- Permanent policy:

  ausearch -m avc -ts recent | audit2allow -M mdcore-engines
  sudo semodule -i mdcore-engines.pp
  sudo restorecon -Rv /var/lib/ometascan/engines

### [**Verification**](/docs/mdcore/v5.22.0/knowledge-base/why-are-metadefender-core-appsec-engines-failing-to-load-after-r#verification)

- `engines` directory repopulates.
- Engine self-tests pass; logs show successful startup/handshake.
- No new SELinux AVCs; mount for engines shows `exec`.

### [**Best Practices**](/docs/mdcore/v5.22.0/knowledge-base/why-are-metadefender-core-appsec-engines-failing-to-load-after-r#best-practices)

- Keep engines on a filesystem mounted with `exec`; bind-mount if `/var` must be `noexec`.
- Preinstall RHEL 9 runtime libraries on Core nodes.
- Validate SELinux contexts/policies on hardened builds.

Support:

If Further Assistance is required, please proceed to log a [support case or chat with our support engineer at <https://my.opswat.com/support>.

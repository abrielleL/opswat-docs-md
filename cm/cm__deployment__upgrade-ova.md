<!-- source: https://www.opswat.com/docs/cm/deployment/upgrade-ova -->

# Upgrade

> **Info**
>
> Note that due to to how we structure the ova’s cm10 app, bootc upgrade will only apply OS updates and /opt/mocm template folder changes, **not the working folder /var/opt/mocm**

1. Download new bootc image archive mocm.tar.zst from bootc image build

![](https://uploads.developerhub.io/prod/97qW/5iimy4tdqypomziishvkcogr2hthkn6yjvcx9qfqrafmi9z7p1oxbbfu1l5d137m.png)

2. Run as root

```typescript
sudo -s
```

3. In the VM, run **bootc switch --transport oci-archive <full path to mocm.tar.zst>** An error “unsupported transport oci-archive for looking up local images” may appear, this is normal. bootc seems to check if the target path is an image first before parsing the --transport parameter

![](https://uploads.developerhub.io/prod/97qW/cn59k785npzc754xt24zbpz2j3c3atypjxsl9kwpb1zj495s98oaf5s0nbjw63lk.png)

- As long as the archive image is queued for the next boot, it should be okay to proceed.

4. Restart machine

```typescript
reboot
```

5. On next boot, updates are applied to the OS and the /opt/mocm folder
6. Stop and disable mocm services

```typescript
systemctl stop redis nginx rabbitmq-server mocm-all.target
systemctl disable mocm-all.target
```

7. Rerun **/opt/mocm/lib/init-filesystem.sh** to apply the new changes Currently, may remove some user-applied changes (anything that is not written in template .tpl format setting files or not located in /etc/opt/mocm/, which is the designated folder for user-specific setting files)
8. Reboot after applying the relabel changes.

```typescript
reboot
```

9. Start mocm services

```typescript
systemctl start mocm-all.target
#Enable mocm-all.target to auto-start on boot
systemctl enable mocm-all.target
```

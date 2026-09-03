<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/configuration/dongles -->

# Security Dongles

### [Security Dongles](/docs/netwall/v5.13.2/configuration/dongles#security-dongles)

MetaDefender Security Gateway includes two USB devices (security dongles). OPSWAT encrypts each dongle with information unique to your site. The dongles are encrypted and configured so they cannot be accessed from a computer by normal means. Each dongle contains the following information that is unique for each customer:

- A Site Key identifies your organization’s site. This Key is the same on all your dongles.
- A security key unique to each dongle.

Dongles needs to be register to work properly. MetaDefender Security Gateway user will be provided with two pre-registered dongles. If users want to acquire extra dongles, OPSWAT will provide them with instruction to perform the registration of the new dongles.

In order to perform configuration changes in one of the sides using the web UI, one of the dongles should be inserted in the corresponding server, BLUE or RED.

If no dongle is inserted a user can login in the web UI for BLUE and RED sides, but can not chage configuration changes.

### [Registering Dongles](/docs/netwall/v5.13.2/configuration/dongles#registering-dongles)

Registering a dongle is done on the MetaDefender Security Gateway CLI. You can access the CLI over SSH ( if its enabled) or by attaching a Keyboard and Monitor to the server.

Plug in a dongle and follow the steps below. **Note: ?** will get you a list of available commands

BashCopynetwall> dongle
netwall (dongle)> register
Dongle Number: 1080
Dongle Site ID: e5d4877b-5923-421c-848c-bfbcc3366dfd
Do you want to register this dongle ?
Continue? [y/N] y
netwall (dongle)> list
You can delete any dongle by its ID
ID: 1042 Site ID: e5d4877b-5923-421c-848c-bfbcc3366dfd
ID: 1080 Site ID: e5d4877b-5923-421c-848c-bfbcc3366dfd
netwall (dongle)>

After a dongle is registered, it must be pulled out and inserted back in before attempting any configuration updates.

<!-- source: https://www.opswat.com/docs/mdtransferguard/configuration/2-metadefender-optical-diode-dongles -->

# Security Dongles

### [Security Dongles](/docs/mdtransferguard/configuration/2-metadefender-optical-diode-dongles#security-dongles)

MetaDefender Diode X includes two USB devices (security dongles). OPSWAT encrypts each dongle with information unique to your site. The dongles are encrypted and configured so they cannot be accessed from a computer by normal means. Each dongle contains the following information that is unique for each customer:

- A Site Key identifies your organization’s site. This Key is the same on all your dongles.
- A security key unique to each dongle.

Dongles needs to be registered to work properly. Diode X ships with two pre-registered dongles.

When performing configuration changes in either the BLUE or RED sides, a dongle must be inserted in the corresponding server, BLUE or RED .

If no dongle is inserted, a user can login in the web UI for BLUE and RED sides, but can not change configuration.

### [Registering Dongles](/docs/mdtransferguard/configuration/2-metadefender-optical-diode-dongles#registering-dongles)

In the event that additional dongles are requested or replaced, the new dongles must be registered following the instruction below.

Registering a dongle is done on the Diode X CLI. You can access the CLI over SSH ( if its enabled) or by attaching a Keyboard and Monitor to the server.

Plug in a dongle and follow the steps below. **Note: ?** will get you a list of available commands

BashCopynetwall> dongle
netwall (dongle)> register
Dongle Number: 1080
Dongle Site ID: e5d4877b-5923-421c-848c-bfbcc3366dfd
Do you want to register this dongle ?
Continue? [y_N] y
netwall (dongle)> list
You can delete any dongle by its ID
ID: 1042 Site ID: e5d4877b-5923-421c-848c-bfbcc3366dfd
ID: 1080 Site ID: e5d4877b-5923-421c-848c-bfbcc3366dfd
netwall (dongle)>

After a dongle is registered, it must be pulled out and inserted back in before attempting any configuration updates.

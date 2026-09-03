<!-- source: https://www.opswat.com/docs/myop/knowledge-base/list-of-available-cli-commands -->

# List of Available CLI Commands a local user can execute

In our virtual appliance, local users that are created during the Setup process can execute various commands via command line interface (CLI) to perform tasks and manage the system. There are restricted commands that are limited for security considerations.

Below is a list of commands that a user is allowed to execute from the command line:

- docker
- ifconfig
- ip
- traceroute
- ping
- dig
- nslookup
- hostname
- netstat
- openssl
- top
- lsof
- bash
- adduser
- userdel
- addgroup
- delgroup
- usermod
- reboot
- shutdown
- init
- halt
- ssh
- ssh-keygen
- ssh-copy-id
- df
- du
- lsblk
- lsof
- curl

The following scripts are also available. Note that all scripts must be run with sudo privilege

- sudo /os/prod-scripts/cent-generate-sup-package.sh

  - Generate a support package used for troubleshooting in the current folder.
- sudo /os/prod-scripts/cent-cleanup-sup-package.sh

  - Clean up all previously generated support packages.
- sudo /os/prod-scripts/cent-ocm-service.sh <stop/start>

  - Stop or start My OPSWAT service.

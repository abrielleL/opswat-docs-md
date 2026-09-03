<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/tacacs -->

# TACACS+ Configuration

While TACACS+ support is not yet implemented in the web console, it is still possible to use your MetaDefender NAC Edge VM as a TACACS server via direct CLI configuration. Instructions on how to do this are provided below.

### Get to the bash shell

First you will need SSH access to the NAC Edge VM. Instead of logging in as the `admin`  user (which would bring up the initial setup TUI], you will need to log in as the `nac`  user. If you don't have the password for this user, please contact OPSWAT support.

### Create the "tac_plus-ng.cfg" config file

For this guide we'll add a Docker container to the NAC Edge VM which will run a "tac_plus-ng" docker container alongside the docker containers that ship with the VM image.

The first step is to create a "tac_plus-ng.cfg" file with settings appropriate for your environment:

```bash
cd
mkdir tacacs/etc/
nano tacacs/etc/tac_plus-ng.cfg
```

Paste in the following contents. (Be sure to edit the LDAP settings on lines 40-45 and `key`  value on line 69 as appropriate for your environment.)

```plaintext
#!/usr/local/sbin/tac_plus-ng

id = spawnd {
    listen = {
        port = 49
    }

    spawn = {
        instances min = 1
        instances max = 10
    }

    background = no
}

id = tac_plus-ng {
    #
    # Logging
    #
    log authzlog { destination = /var/log/tac_plus-ng_authz.log }
    log authclog { destination = /var/log/tac_plus-ng_authc.log }
    log acctlog  { destination = /var/log/tac_plus-ng_acct.log }

    accounting    log = acctlog
    authentication log = authclog
    authorization  log = authzlog

    #
    # MAVIS group handling
    #
    mavis module = groups {
        # Only pass through these groups; they are mapped below
        groups filter = /^(NetworkAdmins|NetworkGuests)$/
        # memberof filter = /^CN=tacacs_/   # example prefix filter (disabled)
    }

    #
    # MAVIS LDAP backend
    #
    mavis module = external {
        setenv LDAP_SERVER_TYPE            = "microsoft"
        setenv LDAP_HOSTS                  = "192.168.99.101:389"
        setenv LDAP_BASE                   = "dc=mgmlab,dc=local"
        setenv LDAP_USER                   = "Administrator@mgmlab.local"
        setenv LDAP_PASSWD                 = "MY_VERY_SECRET_PASSWORD"
        setenv TACACS_GROUP_PREFIX         = ""
        setenv UNLIMIT_AD_GROUP_MEMBERSHIP = 1
        setenv REQUIRE_TACACS_GROUP_PREFIX = 0

        exec = /usr/local/lib/mavis/mavis_tacplus_ldap.pl
    }

    #
    # Use MAVIS for all authentication backends
    #
    login backend = mavis
    user  backend = mavis
    pap   backend = mavis

    #
    # Global host definition
    #
    host world {
        address       = 0.0.0.0/0, ::/0
        welcome banner = "******************* Welcome to DEMO TACACS+ NG *************\
"
        enable 15     = clear SECRET_ENABLE_PASSWORD
        anonymous-enable = deny        # always authenticate on enable
        key           = "SECRET_TACACS_ENCRYPTION_PASSWORD"
    }

    #
    # Admin profile – full privilege (15)
    #
    profile admins {
        script {
            if (service == shell) {
                if (cmd == "") {
                    set priv-lvl = 15
                    permit
                }
                permit
            }
        }
    }

    #
    # Operator profile – restricted commands
    #
    profile operators {
        script {
            if (service == shell) {

                # Initial login privilege
                if (cmd == "") {
                    set priv-lvl = 15
                    permit
                    return
                }

                # Allow enable
                if (cmd =~ /^enable/) {
                    permit
                    return
                }

                # Block configuration commands
                if (cmd =~ /^config/) {
                    deny
                    return
                }

                # Allow show commands
                if (cmd =~ /^show/) {
                    permit
                    return
                }

                # Deny all other commands
                deny
            }
        }
    }

    #
    # Group declarations
    #
    group admins
    group operators

    #
    # Rules – map LDAP group to TACACS+ profile
    #
    ruleset {
        rule {
            script {
                if (memberof =~ /NetworkAdmins/) {
                    message = "Debug: User belongs to groups: ${memberof}"
                    profile = admins
                    permit
                    return
                }

                if (memberof =~ /NetworkOperator/) {
                    message = "Debug: User belongs to groups: ${memberof}"
                    profile = operators
                    permit
                    return
                }

                # User not in a handled group
                deny
            }
        }
    }
}
```

This example configuration

- Authenticates users against an LDAP Server at `192.168.99.101`
- Defines the profiles
  - `admins`  where users have privilege level 15
  - operators where users have privilege level 1
- Defines mappings
  - AD Group `NetworkAdmins` -> profile `admins`
  - AD Group `NetworkOperator`  -> profile `operators`

### Start the container

Edit `~/docker-compose.yml`

```bash
nano ~/docker-compose.yml
```

Add the following service definition to the end of the file. (Keep indentation)

```yaml
tac_plus-ng:
    image: christianbecker/tac_plus-ng
    volumes:
      - /home/nac/tacacs/etc/tac_plus-ng.cfg:/usr/local/etc/tac_plus-ng.cfg:ro
      - /var/log/:/var/log/
    ports:
      - 49:49/tcp
```

Save the file and run the following command to bring up the new container/service

```bash
docker compose up -d
```

### Configure the networking device for AAA for CLI users

The specific commands may vary by the specific model and firmware version of your networking device. Below is for a Cisco switch running IOS 15+

```plaintext
aaa new-model
!
aaa authentication login default group tacacs+ local
aaa authentication enable default group tacacs+
aaa authorization exec default group tacacs+ local
aaa authorization commands 1 default group tacacs+ local
aaa authorization commands 15 default group tacacs+ local
aaa accounting exec default start-stop group tacacs+
aaa accounting commands 1 default start-stop group tacacs+
aaa accounting commands 15 default start-stop group tacacs+
!
tacacs server TACACS+
 address ipv4 192.168.99.100
 key SECRET_TACACS_ENCRYPTION_PASSWORD
```

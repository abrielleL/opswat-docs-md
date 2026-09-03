<!-- source: https://www.opswat.com/docs/manac/knowledge-base/how-to-set-up-lab-machines-for-use-with-nac -->

# How to set up Lab Machines for use with NAC?

This article applies to the current NAC Enforcer and Web UI, as well as all Windows and MacOS systems running the latest NAC Policy Key.

User identity is of the utmost importance when using NAC in a lab environment, which is why the system provides streamlined solutions for both capturing and verifying the identities of both AD/LDAP users and guest users.

To facilitate optimal, secure processes when using NAC in a lab environment with a range of users, please follow the relevant best practice steps below.

## [Windows and macOS domain machines](/docs/manac/knowledge-base/how-to-set-up-lab-machines-for-use-with-nac#windows-and-macos-domain-machines)

1. For these machines, a **Policy Group** should be created that includes the relevant domain attributes.

- Navigate to your **NAC Dashboard>Policies>Group**.
- Click the **New** button in the left-hand panel.
- Fill out the necessary details, then click **Apply and Use**.

2. Create a new authenticaiton policy for this group and set the Authentication Type to **“Every session provided 0 hours have passed”**

3. Either the **Policy Key** must be pre-deployed to distinguish the lab machines from non-domain machines, or the **ADConnector** must be installed on all domain controllers.
4. Users must log off the desktop at the end of every lab machine session.
5. For guest users, a local machine account should be created that allows access to the desktop.

   - Once logged in, guest users will either need to complete a **Self-Registration** process, which can be configured via the **NAC Dashboard>Configuration>Self-Enrollment Portals>Guest Self-Provisioning Setup**, as shown below:

- Or they can log into NAC via a Sponsored Guest Account, or log into the network via the one-click Anonymous Access method. - A startup script can easily be added to the local machine account, that opens a web browser directly onto the appropriate NAC page.

## [All other devices](/docs/manac/knowledge-base/how-to-set-up-lab-machines-for-use-with-nac#all-other-devices)

1. If these devices are in a dedicated VLAN, the **IP Range** for that VLAN should be configured as the **Qualifier** for access.
2. If these devices are not in a dedicated VLAN, a **Policy Group** that includes MAC addresses for the lab machines should be created.

- Navigate to your **NAC Dashboard>Policies>Group**.
- Click the **New** button in the left-hand panel.
- Fill out the necessary details, then click **Apply and Use**.

3. Create a new authenticaiton policy for this group and set the Authentication Type to **“Every session provided 0 hours have passed”**

4. A link to the [Logout Page](https://portal.myweblogon.com:8443/html/logout.htm) will need to be placed on the desktop or home screen.
5. Users will need to click the logout link and log out of NAC at the end of every lab machine session.
6. Guest users will either need to complete a **Self-Registration** process, which can be configured via the **NAC Dashboard>Configuration>Self-Enrollment Portals>Guest Self-Provisioning Setup**, as shown below:

7. Or they can log into NAC via a **Sponsored Guest Account** or log into the network via the one-click **Anonymous Access** method.

Support:

If you have followed the instructions above but have been unable to **Set Up One Or More Lab Machines For NAC**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

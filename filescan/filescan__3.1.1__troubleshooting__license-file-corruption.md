<!-- source: https://www.opswat.com/docs/filescan/3.1.1/troubleshooting/license-file-corruption -->

# License file corruption

Under heavy load or due to limited disk space, some I/O operations might fail and Sandbox might not be able to complete scan tasks. In these situations, it might be impossible for Sandbox to write log files or temporary files to disk.

Unfortunately, this can also lead to the **corruption** of the `license.dat` file in the `/home/sandbox/sandbox/transform/license` folder.

When the `sandbox` service is restarted, the corrupted license data cannot be loaded and no scan operations can be completed until the license is restored.

When this issue occurs, the `transform.log` file (in `/home/sandbox/sandbox/logs`) typically contains entries like the following:

transform.logCopy[{}] main 2024-12-02 08:10:30,936 WARN 174 [b] - Could not read license data from disk. First run?
java.io.EOFException: null
at java.base/java.io.ObjectInputStream$BlockDataInputStream.peekByte(ObjectInputStream.java:3214) ~[?:?]
at java.base/java.io.ObjectInputStream.readObject0(ObjectInputStream.java:1684) ~[?:?]
at java.base/java.io.ObjectInputStream$FieldValues.<init>(ObjectInputStream.java:2606) ~[?:?]
at java.base/java.io.ObjectInputStream.readSerialData(ObjectInputStream.java:2457) ~[?:?]
at java.base/java.io.ObjectInputStream.readOrdinaryObject(ObjectInputStream.java:2257) ~[?:?]
at java.base/java.io.ObjectInputStream.readObject0(ObjectInputStream.java:1733) ~[?:?]
at java.base/java.io.ObjectInputStream.readObject(ObjectInputStream.java:509) ~[?:?]
at java.base/java.io.ObjectInputStream.readObject(ObjectInputStream.java:467) ~[?:?]
at fsio.transform.license.b.f(LicenseService.java:172) [transform.jar:?]
at fsio.transform.license.b.b(LicenseService.java:65) [transform.jar:?]
at fsio.transform.Main.a(Main.java:267) [transform.jar:?]
at fsio.transform.Main.main(Main.java:210) [transform.jar:?]
...
[{}] pool-8-thread-3 2024-12-02 08:10:51,105 WARN 76 [b] - No valid license found
[{}] pool-8-thread-3 2024-12-02 08:10:51,106 WARN 197 [b] - No license file provided
[{}] pool-8-thread-3 2024-12-02 08:10:51,106 ERROR 81 [b] - Scan request not authorized, license state: UNAVAILABLE, limit: 0, count: 0
[{}] pool-8-thread-3 2024-12-02 08:10:51,106 ERROR 203 [f] - Failed to execute scan on input file (no valid license)
## [Remediation](/docs/filescan/3.1.1/troubleshooting/license-file-corruption#remediation)

If this issue occurs once, it might be sufficient to restore the license manually following the [License Activation](/docs/filescan/3.1.1/installation/license-activation) guide.

If the issue occurs **repeatedly**, then a permanent solution is adding the `license.yml` file in the `/home/sandbox/sandbox/transform/license` folder.

The license be re-activated automatically when a valid `license.yml` is detected.

### [Remediation steps in an online environment:](/docs/filescan/3.1.1/troubleshooting/license-file-corruption#remediation-steps-in-an-online-environment)

- Create a file named `license.yml` in your Sandbox installation directory: `/home/sandbox/sandbox/transform/license/license.yml` (the path might be different if you installed Sandbox to a different target directory)
- Copy **your activation key** to the newly created `license.yml` file

Example license.yml containing a dummy activation keyCopyxxxx-xxxx-xxxx-xxxx-xxxx-xxxx-xxxx-xxxx

You can also use these commands to accomplish this:

BashCopyecho "ACTIVATION_KEY" > ~/license.yml
sudo cp ~/license.yml /home/sandbox/sandbox/transform/license/
### [Remediation steps in an offline environment:](/docs/filescan/3.1.1/troubleshooting/license-file-corruption#remediation-steps-in-an-offline-environment)

- Use the **offline license file** that you have previously downloaded from your [My OPSWAT](https://my.opswat.com) portal.
- Copy your offline license file to the Sandbox installation directory: `/home/sandbox/sandbox/transform/license/license.yml` (the path might be different if you installed Sandbox to a different target directory)

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

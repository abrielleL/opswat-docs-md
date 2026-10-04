<!-- source: https://www.opswat.com/docs/mddrive/configuration/out-of-box-experience-setup -->

# Automate First-Boot Setup with an Ignition File

Use an ignition file to set up a MetaDefender Drive without touching its screen. Write one small INI file to MetaDefender Drive. On the next boot, MetaDefender Drive reads it, joins Wi-Fi, activates its license, enrolls with Central Management, and enrolls for Centralize Profile.

## [Before you begin](/docs/mddrive/configuration/out-of-box-experience-setup#before-you-begin)

- A Windows computer. The data partition of MetaDefender Drive is NTFS, and Windows reads and writes it without extra software.
- The values you want to apply: Central Management address and registration code, a license activation key, Wi-Fi details, and a Centralize Profile approver name.

## [Create the file](/docs/mddrive/configuration/out-of-box-experience-setup#create-the-file)

MetaDefender Drive does not ship with an ignition file. Create one yourself:

1. Connect MetaDefender Drive to your computer.
2. Open the `configuration` folder on the data partition of MetaDefender Drive (`<drive>:\configuration`).
3. Create a file named exactly `mdd_ignition.ini`, in lowercase.
4. Add the sections you need (see below). Leave out any section you do not want to apply.
5. Safely eject MetaDefender Drive and boot it.

Important
> The file name must be exactly `mdd_ignition.ini`, in lowercase, in the `configuration` folder. A file named `MDD_Ignition.ini`, or `mdd_ignition.ini.txt` (Notepad adds `.txt` when you save), is deleted at boot without any message. In Windows File Explorer, turn on **File name extensions** (View > Show) so you can see the real file name.

Note
> At boot, MetaDefender Drive deletes files it does not recognize on the data partition. Do not store other files in the `configuration` folder, because they can be deleted. MetaDefender Drive keeps `mdd_ignition.ini`, its own configuration files, and any file whose name ends in `.pem`, `.crt`, `.cer`, `.cert`, or `.der` (not case-sensitive), so a Wi-Fi CA certificate you place there survives.

## [Example](/docs/mddrive/configuration/out-of-box-experience-setup#example)

This is a complete template. Every setting starts with `;`, which makes it a comment. Remove the `;` from each setting you want to use and replace the placeholder values. Write a comment on its own line: a comment placed after a value on the same line is not supported.

; Remove the ; to use a setting. Comments must be on their own line.
[MO]
; url must start with http:// or https://. "registration_code" = alias of regcode.
;url=https://cm.example.com
;regcode=REPLACE-WITH-YOUR-REGISTRATION-CODE
;accept_self_signed=true
[LICENSE]
; "key" = alias of activation_key.
;activation_key=XXXX-XXXX-XXXX-XXXX
[NETWORK]
;ssid=Corp-WiFi
;password=REPLACE-WITH-THE-WIFI-PASSWORD
; auto (default) | open | wpa-psk | wpa-sae | wpa-eap
;security=auto
;hidden=false
;autoconnect=true
; WPA/WPA2-Enterprise only (username/password; EAP-TLS not supported).
; "username" = alias of identity.
;identity=user@corp.example.com
; peap (default) | ttls
;eap=peap
; mschapv2 (default) | pap | gtc
;phase2=mschapv2
;anonymous_identity=anonymous@corp.example.com
;domain=radius.corp.example.com
; CA file name in this folder, ending in .pem/.crt/.cer/.cert/.der.
; Named but missing or invalid = Wi-Fi is not joined.
;ca_cert=corp-radius-ca.pem
[OTP]
; Enrolls only when enroll=true AND the [MO] server accepts the regcode.
;enroll=true
; Default: "MDD: <serial number>".
;approver=Name Of The Approving Person
## [What happens at boot](/docs/mddrive/configuration/out-of-box-experience-setup#what-happens-at-boot)

1. MetaDefender Drive joins the Wi-Fi network from `[NETWORK]`, because Centralize Profile enrollment, license activation, and Central Management need a connection. Centralize Profile enrollment checks that Central Management can be reached before it enrolls. MetaDefender Drive joins even when an Ethernet cable is plugged in.
2. MetaDefender Drive enrolls for Centralize Profile from `[OTP]`, but only when `enroll=true` and the Central Management server from `[MO]` answers. If it cannot be reached, MetaDefender Drive skips Centralize Profile enrollment and scans run without the one-time password gate.
3. MetaDefender Drive activates the license from `[LICENSE]`, but only when it has no working license. If the key is rejected, MetaDefender Drive shows a warning and then falls back to its normal automatic activation.
4. MetaDefender Drive enrolls with Central Management from `[MO]`. MetaDefender Drive skips this step when it is already enrolled, or when an enrollment is pending (set up by the Toolkit or the SMC).
5. MetaDefender Drive deletes `mdd_ignition.ini`, even if an earlier step failed. Nothing is retried on the next boot.

## [Sections and keys](/docs/mddrive/configuration/out-of-box-experience-setup#sections-and-keys)

### [[MO] — Central Management](/docs/mddrive/configuration/out-of-box-experience-setup#mo--central-management)

| Key | Required / Optional | Description |
| --- | --- | --- |
| `url` | Required | Address of the Central Management server, for example `https://cm.example.com`. It must start with `http://` or `https://`. |
| `regcode` | Required | Registration code issued by Central Management. `registration_code` is accepted as an alias. |
| `accept_self_signed` | Optional | Set to `true` to trust a self-signed Central Management certificate. Default: not set. |

- Both `url` and `regcode` are required.
- If MetaDefender Drive already has a working Central Management enrollment, or an enrollment is pending (set up by the Toolkit or the SMC), the file is ignored for enrollment. The existing enrollment wins.
- If the server presents a self-signed certificate that MetaDefender Drive does not already trust, enrollment is refused unless `accept_self_signed=true`. MetaDefender Drive never prompts at boot, because nobody is there to answer. When you enroll from the user interface instead, MetaDefender Drive asks you whether to trust the certificate.

### [[LICENSE] — License activation](/docs/mddrive/configuration/out-of-box-experience-setup#license--license-activation)

| Key | Required / Optional | Description |
| --- | --- | --- |
| `activation_key` | Required | The license activation key. `key` is accepted as an alias. |

### [[NETWORK] — Wi-Fi](/docs/mddrive/configuration/out-of-box-experience-setup#network--wi-fi)

| Key | Required / Optional | Description |
| --- | --- | --- |
| `ssid` | Required | Name of the Wi-Fi network. |
| `password` | Required for `wpa-psk`, `wpa-sae`, and `wpa-eap` | Wi-Fi password (`wpa-psk`, `wpa-sae`), or the user's password (`wpa-eap`). |
| `security` | Optional | `auto` (default), `open`, `wpa-psk`, `wpa-sae`, or `wpa-eap`. |
| `hidden` | Optional | `true` for a network that does not broadcast its name. Default: `false`. |
| `autoconnect` | Optional | Set to `false` to save the network without joining it automatically on later boots. Default: `true`. |
| `identity` | Required for `wpa-eap` | User name for WPA/WPA2-Enterprise (802.1X). `username` is accepted as an alias. |
| `eap` | Optional | Outer method: `peap` (default) or `ttls`. |
| `phase2` | Optional | Inner authentication: `mschapv2` (default), `pap`, or `gtc`. |
| `anonymous_identity` | Optional | Outer identity sent in clear before the tunnel is up. |
| `domain` | Optional | The RADIUS server certificate must be issued for this domain or a subdomain of it. |
| `ca_cert` | Optional (recommended) | File name of the CA certificate (PEM or DER) that issued the RADIUS server certificate. |

Notes:

- With only `ssid` and `password`, MetaDefender Drive detects the security type itself.
- A hidden network cannot be detected. With `hidden=true` and no `security`, MetaDefender Drive assumes `wpa-psk` when a password is given, and `open` when it is not. Set `security=wpa-sae` for a hidden WPA3-only network.
- If you set `identity`, the network is treated as WPA/WPA2-Enterprise.
- Only username and password methods are supported. EAP-TLS (client certificate) is not supported.
- To use `ca_cert`, place the certificate next to the ignition file (`<drive>:\configuration\<name>`). The file name must end in `.pem`, `.crt`, `.cer`, `.cert`, or `.der`. MetaDefender Drive copies the certificate to its own storage and leaves your original in place.
- `ca_cert` is used only with `wpa-eap`. On any other security type it is ignored.
- If `ca_cert` is named but the file is missing or is not a certificate, MetaDefender Drive does not join the network. Without `ca_cert`, the server certificate is not validated, and the password goes to whichever server answers.
- MetaDefender Drive joins the network even if an Ethernet cable is already connected. Both links stay active, and the wired connection remains the preferred route.
- A wrong password costs one bounded timeout at boot. It does not hang MetaDefender Drive.

### [[OTP] — Centralize Profile enrollment](/docs/mddrive/configuration/out-of-box-experience-setup#otp--centralize-profile-enrollment)

The section is named `[OTP]` in the file.

| Key | Required / Optional | Description |
| --- | --- | --- |
| `enroll` | Required | Set to `true` to enroll MetaDefender Drive for Centralize Profile. |
| `approver` | Optional | Name of the approver. Default: `MDD: <serial number>`. |

- MetaDefender Drive enrolls only when `enroll=true` **and** Central Management answers successfully with the registration code. `[MO]` must therefore be present and correct.
- Leave `approver` out to name MetaDefender Drive after its serial number. Each drive then has a distinct name in the approver list. Name a person only when one person owns the drive.
- If Central Management does not answer, MetaDefender Drive skips enrollment and scans run without the one-time password gate.
- Enrollment happens once. MetaDefender Drive does not enroll again on later boots, so the authenticator your approver registered stays valid.
- After enrollment, scans, file copies, and report deletion require a one-time password.
- MetaDefender Drive creates the secret itself, so nobody holds it yet. Central Management supplies the real approver and secret afterwards. This is why MetaDefender Drive enrolls only when Central Management answers.

## [After boot](/docs/mddrive/configuration/out-of-box-experience-setup#after-boot)

- MetaDefender Drive deletes `mdd_ignition.ini` once every step has been attempted. The file holds the registration code, the activation key, and the Wi-Fi password in clear text, so it does not stay on MetaDefender Drive.
- MetaDefender Drive applies the file once and then removes it, so there is nothing to read on the next boot. To apply the settings again, write the file again and reboot.
- A failed Central Management enrollment and a rejected license key are shown as notifications, not dialogs. Wi-Fi and Centralize Profile failures are only written to the log.

## [Troubleshooting](/docs/mddrive/configuration/out-of-box-experience-setup#troubleshooting)

| Symptom | Cause and fix |
| --- | --- |
| The file was not applied and is gone. | Either MetaDefender Drive consumed it on the previous boot, or the file name was not exactly `mdd_ignition.ini` (for example `MDD_Ignition.ini` or `mdd_ignition.ini.txt`) and it was deleted without a message. Turn on file name extensions in File Explorer and write the file again. |
| MetaDefender Drive does not enroll with Central Management. | Check that `url` and `regcode` are both set and that the server is reachable. For a self-signed certificate, set `accept_self_signed=true`. An existing or pending enrollment also makes MetaDefender Drive skip `[MO]`. |
| MetaDefender Drive is not enrolled for Centralize Profile. | Check that `enroll=true` and that Central Management answered. Enrollment is skipped when it does not. |
| MetaDefender Drive does not join Wi-Fi. | Check the password and `security`. For a hidden network, set `hidden=true` and `security` explicitly. If `ca_cert` is set, check that the file exists and is a valid certificate. |

## [Related topics](/docs/mddrive/configuration/out-of-box-experience-setup#related-topics)

- [Activate License](https://www.opswat.com/docs/mddrive/getting-started/activate-license)
- [Enroll MetaDefender Drive to Central Management Server from MetaDefender Drive User Interface](https://www.opswat.com/docs/mddrive/configuration/enroll-cm-from-drive)
- [Centralized Scanning Profile](https://www.opswat.com/docs/mddrive/configuration/centralized-scanning-profile)

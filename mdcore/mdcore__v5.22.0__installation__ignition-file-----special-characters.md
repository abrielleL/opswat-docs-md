<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters -->

# Ignition file - special characters

## [Overview](/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters#overview)

The **ignition file** automates first-time setup of MetaDefender Core (EULA, admin account, database, HTTPS, and more). It uses INI-style `key=value` lines under sections such as `[user]` and `[dbserver]`.

Some characters have special meaning. If a password or passphrase contains them and is not written correctly, MetaDefender Core may read a **truncated or wrong value** without a clear error message.

### [Default file location](/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters#default-file-location)

- **Windows:** `c:\opswat\ometascan.conf`
- **Linux:** `/etc/opswat/ometascan.conf`

## [Be careful — the most common mistake](/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters#be-careful--the-most-common-mistake)

A **semicolon (**`;`**)** inside an unquoted password is treated as the start of a comment. Everything after `;` on that line is ignored.

## [Fields to watch](/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters#fields-to-watch)

Check these ignition-file fields carefully when values contain special characters:

- `[user] password`, `[user] apikey`
- `[dbserver] password`, `[dbserver] private_password`
- `[config] import_password`
- `[https] passphrase`

## [Special characters](/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters#special-characters)

| **Character** | **Why it matters** | **What to do** |
| --- | --- | --- |
| `;` | Comment / ends unquoted values | Wrap the whole value in `"..."`. **Do not** use `\;`. |
| `=` | Separates key and value | Wrap in quotes if `=` appears inside the value. |
| `"` | Quote delimiter | Wrap in quotes; escape inner quotes as `\"`. |
| `\` | Escape prefix | Write a literal backslash as `\\`. |
| `,` | List separator | Wrap in quotes if comma is part of the value. |
| `#` | No special meaning | Normal character — no extra escaping needed. |

## [How to write passwords safely](/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters#how-to-write-passwords-safely)

1. If the value contains `;`, `=`, or `,` — wrap it in **double quotes**.
2. Never use `\;` to escape a semicolon — it does **not** work.
3. Escape `\` as `\\` and `"` as `\"`.
4. Quote-doubling (`""`) is **not** supported — use `\"` instead.

## [Examples](/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters#examples)

### [Password with semicolon](/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters#password-with-semicolon)

Intended password: `Ew6I]7;a:SRD`

BashCopy[user]
name=admin
password="Ew6I]7;a:SRD"
email=admin@local
### [Password with semicolon and double quote](/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters#password-with-semicolon-and-double-quote)

Intended password: `Say;"hello"`

BashCopy[user]
password="Say;\"hello\""
### [Database password](/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters#database-password)

BashCopy[dbserver]
password="p@ss;w=rd"
## [Quick reference](/docs/mdcore/v5.22.0/installation/ignition-file-----special-characters#quick-reference)

| Value contains… | Do this |
| --- | --- |
| `;` | Wrap in `"..."` — not `\;` |
| `"` | Wrap in quotes; use `\"` for each inner quote |
| `\` | Write `\\` |
| `;` and `"` | Quotes around value + `\"` for inner quotes |

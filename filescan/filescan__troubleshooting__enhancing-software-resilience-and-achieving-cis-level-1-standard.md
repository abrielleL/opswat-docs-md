<!-- source: https://www.opswat.com/docs/filescan/troubleshooting/enhancing-software-resilience-and-achieving-cis-level-1-standard -->

# Enhancing Software Resilience and Achieving CIS Level 1 Standards

Apart from regular Ubuntu, Sandbox can also run on CIS level 1 hardened Ubuntu.

To harden the operating system first, please use the guide from here: <https://www.open-scap.org/security-policies/scap-security-guide/>

The upcoming guide will be divided into two different sections:

1. Steps to make the installer antivirus-compliant
2. Fixing post-installation issues, related to the hardened OS

**Steps to make the installer antivirus-compliant**

Info

You can run this step both before and after the installation, whether you need the installer ZIP compliant or only the installed software itself.

In this section, we will unpack the installer and run a script to modify potentially falsely detected files and malware rules.

1. Download the latest release from the OPSWAT Portal
2. If you have internet connection: run the following command: `pip3 install plyara`
3. Do the first step described on the following link: [installation/offline-installation](https://docs.opswat.com/filescan/installation/offline-installation) (unpack the zip)
4. Using the same command as previously, but now unpack the `sandbox.zip` file as well *(It's in the sandbox-installer directory that you just unzipped)*
5. Now you have a directory inside, called `sandbox`. Grab the Python script `harden-yara.py` which you can find below. Copy it next to the `sandbox` directory.
6. Execute the python script using the following command: `python3 harden_yara.py sandbox/transform/yara/rules`
7. Execute the python script using the following command: `python3 harden_yara.py sandbox/webservice/src/storage/resources/yara_rules`
8. Execute the python script using the following command: `python3 harden_yara.py sandbox/transform/parser/mwconfig-extractors`
9. Now re-zip the `sandbox` directory and you're done. Example Linux command: `7z a -r sandbox.zip sandbox`
10. Now you can proceed on installing Sandbox either in an online or offline manner

Warning

**Below, you can find two different scripts.** If you can install plyara pip package, please use the first script, else please use the second!

*The version using plyara is more sophisticated, hence it's preferred, however both should work perfectly fine.*

harden-yara.py (first)Copyimport os
import argparse
import plyara
from plyara.utils import rebuild_yara_rule
def string_to_hex_array(s, encoding='ascii'):
if 'wide' in encoding:
return " 00 ".join(f"{ord(c):02X}" for c in s) + " 00"
return " ".join(f"{ord(c):02X}" for c in s)
def process_yara_ruleset(yara_ruleset, strip_comments=True):
hex_ruleset = ''
modifications = []
yara_parser = plyara.Plyara()
try:
rules = yara_parser.parse_string(yara_ruleset)
except:
# invalid yara ruleset
modifications.append("[Parsing error] Removed file content due to invalid YARA syntax")
hex_ruleset = "// Removed content due to invalid YARA syntax" # leave a comment in the yara file
return hex_ruleset, modifications
for rule in rules:
try:
modified_strings = {} # <original, [new strings]>
dollar_strings = {} # special case, unnamed string ($), <position, new string>
# Remove all comments from the entire rule, including multi-line comments
if strip_comments and 'comments' in rule:
del rule['comments']
# Convert string to hex
if 'strings' in rule:
i = 0 # used as rule index (needed for unnamed string case)
for string in rule['strings']:
if 'type' in string and 'text' in string['type']:
if 'value' in string:
original_name = string['name']
if not original_name in modified_strings:
modified_strings[original_name] = []
wide, ascii = False, False
if 'modifiers' in string:
wide = 'wide' in string['modifiers']
ascii = 'ascii' in string['modifiers']
del string['modifiers']
if ascii or not wide: # ascii by default when no keywords
ascii_hex_string = string_to_hex_array(string['value'], encoding='ascii')
if ascii_hex_string:
new_string = {}
new_string['name'] = string['name'] + "_ascii"
new_string['type'] = 'hex'
new_string['value'] = f'{{{ascii_hex_string}}}'
if original_name == '$': # unnamed
new_string['name'] = original_name # restore
dollar_strings[i] = new_string
else:
modified_strings[original_name].append(new_string)
modifications.append(f"[{rule['rule_name']}][{original_name}] Converted ASCII string to hex: {string['value']} -> {{{ascii_hex_string}}}")
if wide:
wide_hex_string = string_to_hex_array(string['value'], encoding='wide')
if wide_hex_string:
new_string = {}
new_string['name'] = string['name'] + "_wide"
new_string['type'] = 'hex'
new_string['value'] = f'{{{wide_hex_string}}}'
if original_name == '$': # unnamed
new_string['name'] = original_name # restore
dollar_strings[i] = new_string
else:
modified_strings[original_name].append(new_string)
modifications.append(f"[{rule['rule_name']}][{original_name}] Converted WIDE string to hex: {string['value']} -> {{{wide_hex_string}}}")
i += 1 # rule index
# unnamed special case ($)
# only modify strings section
# no needed to modify conditions since unnamed strings apply only to generic conditions (as 1 of them)
removed = 0
for no_named_string_index in dollar_strings:
rule['strings'].pop(no_named_string_index - removed)
rule['strings'].append(dollar_strings[no_named_string_index])
removed += 1
# add new strings and fix condition
# fix condition no needed in cases wildcards are used ($str*), since we include a suffix
for key in modified_strings:
if not modified_strings[key]: # empty
continue
i = 0 # string index
for string in rule['strings']:
if key in string['name']:
break
i += 1
if len(modified_strings[key]) == 1: # only 1 modifier (ascii or wide)
rule['strings'].insert(i + 1, modified_strings[key][0])
rule['strings'].pop(i) # remove original string
if key in rule['condition_terms']:
name = modified_strings[key][0]['name']
indices = [i for i, x in enumerate(rule['condition_terms']) if x == key]
for idx in indices:
rule['condition_terms'][idx] = name
if '#' + key[1:] in rule['condition_terms']: # count condition (#)
name = '#' + modified_strings[key][0]['name'][1:]
indices = [i for i, x in enumerate(rule['condition_terms']) if x == '#' + key[1:]]
for idx in indices:
rule['condition_terms'][idx] = name
elif len(modified_strings[key]) == 2: # ascii and wide
rule['strings'].insert(i + 1, modified_strings[key][0])
rule['strings'].insert(i + 2, modified_strings[key][1])
rule['strings'].pop(i) # remove original string
if key in rule['condition_terms']:
name1 = modified_strings[key][0]['name']
name2 = modified_strings[key][1]['name']
indices = [i for i, x in enumerate(rule['condition_terms']) if x == key]
added = 0 # dont break indices
for idx in indices:
rule['condition_terms'].insert(idx+1+added, '(')
rule['condition_terms'].insert(idx+2+added, name1)
rule['condition_terms'].insert(idx+3+added, 'or') # either ascii or wide matches
rule['condition_terms'].insert(idx+4+added, name2)
rule['condition_terms'].insert(idx+5+added, ')')
rule['condition_terms'].pop(idx+added) # remove original condition
added += 5 - 1
if '#' + key[1:] in rule['condition_terms']: # count condition (#)
name1 = '#' + modified_strings[key][0]['name'][1:]
name2 = '#' + modified_strings[key][1]['name'][1:]
indices = [i for i, x in enumerate(rule['condition_terms']) if x == '#' + key[1:]]
added = 0 # dont break indices
for idx in indices:
rule['condition_terms'].insert(idx+1+added, '(')
rule['condition_terms'].insert(idx+2+added, name1)
rule['condition_terms'].insert(idx+3+added, '+') # add ascii and wide matches
rule['condition_terms'].insert(idx+4+added, name2)
rule['condition_terms'].insert(idx+5+added, ')')
rule['condition_terms'].pop(idx+added) # remove original condition
added += 5 - 1
# add hardened yara rule
hex_ruleset += rebuild_yara_rule(rule, condition_indents=False) + '\n'
except:
# error hardening a yara rule
# only drop problematic yara rule, not the yara ruleset
if rule and 'rule_name' in rule:
modifications.append(f"[Hardening error] Removed yara rule {rule['rule_name']} due to invalid YARA syntax")
# test hardened yara ruleset
yara_parser = plyara.Plyara() # reset
try:
yara_parser.parse_string(hex_ruleset)
except:
# invalid yara ruleset
modifications.append("[Hardening error] Removed ruleset due to invalid YARA syntax after hardening")
hex_ruleset = "// Content could not be hardened properly" # leave a comment in the yara file
return hex_ruleset, modifications
def process_file(ruleset, input_file, output_file, strip_comments=True):
try:
with open(input_file, 'r', encoding='utf-8') as infile:
ruleset_content = infile.read()
except UnicodeDecodeError:
with open(input_file, 'r', encoding='ISO-8859-1') as infile:
ruleset_content = infile.read()
if ruleset_content:
converted_yara_ruleset, modifications = process_yara_ruleset(ruleset_content, strip_comments=strip_comments)
# always overwrite, since parser removes unnecessary stuff
if converted_yara_ruleset:
with open(output_file, 'w', encoding='utf-8') as outfile:
outfile.write(converted_yara_ruleset)
if modifications:
print(f"Modifications in ruleset: {ruleset}")
for mod in modifications:
print(f"\t{mod}")
def traverse_and_process(input_folder, output_prefix=None, strip_comments=True):
for root, _, files in os.walk(input_folder):
for file in files:
if file.endswith(".yar") or file.endswith(".yara"):
input_file_path = os.path.join(root, file)
if output_prefix:
output_file_path = os.path.join(root, output_prefix + file)
os.makedirs(os.path.dirname(output_file_path), exist_ok=True)
else:
output_file_path = input_file_path
process_file(file, input_file_path, output_file_path, strip_comments)
def delete_files_in_yara_folder(root_dir):
# Walk through the directory tree
for root, dirs, files in os.walk(root_dir):
# Check if 'yara' is in the path
if 'yara' in root.lower():
for file in files:
# Check for specific file extensions (unneeded artefacts)
if file.endswith(('.eml', '.csv', '.txt', '.js')):
file_path = os.path.join(root, file)
try:
os.remove(file_path)
print(f"Deleted: {file_path}")
except Exception as e:
print(f"Failed to delete {file_path}: {e}")
def main():
parser = argparse.ArgumentParser(description="Clean YARA rules to avoid AV detection by converting ASCII strings to hex arrays and stripping comments, deleting unneeded artefacts (optional, enabled by default).")
parser.add_argument("input_folder", help="Path to the input folder containing YARA rule files.")
parser.add_argument("--output-prefix", help="Optional prefix for output files. If not provided, original files are overwritten.", default=None)
parser.add_argument("--strip-comments", action="store_true", help="Strip comments from the entire rule (default: True).", default=True)
parser.add_argument("--delete-unneeded-artefacts", dest="delete_artefacts", action="store_true", default=True,
help="Delete .eml, .csv, and .txt files in folders containing 'yara'. Default is True.")
parser.add_argument("--keep-unneeded-artefacts", dest="delete_artefacts", action="store_false",
help="Do not delete .eml, .csv, and .txt files even if folders contain 'yara'.")
args = parser.parse_args()
traverse_and_process(args.input_folder, output_prefix=args.output_prefix, strip_comments=args.strip_comments)
if args.delete_artefacts:
delete_files_in_yara_folder(args.input_folder)
if __name__ == "__main__":
main()harden-yara.py (second)Copyimport re
import os
import argparse
def string_to_hex_array(s):
return " ".join(f"{ord(c):02X}" for c in s)
def remove_comments_multiline(yara_rule):
"""
Removes all comments (single-line // comments) from a YARA rule,
but preserves them in the meta section.
"""
lines = yara_rule.splitlines()
processed_lines = []
in_meta = False
for line in lines:
if "meta:" in line:
in_meta = True
elif "strings:" in line or "condition:" in line:
in_meta = False
if in_meta or "meta:" in line:
processed_lines.append(line)
else:
processed_lines.append(re.sub(r'(?<!ftp:)(?<!ftps:)(?<!http:)(?<!https:)//.*', '', line).strip())
return "\n".join(processed_lines)
def process_yara_rule(yara_rule, strip_comments=True):
if strip_comments:
# Remove all comments from the entire rule
yara_rule = remove_comments_multiline(yara_rule)
hex_rule = ""
strings_section = False
modified = False
modifications = []
rule_name = None
for line in yara_rule.splitlines():
if "rule " in line:
match = re.search(r'rule\s+(\w+)', line)
if match:
rule_name = match.group(1)
if "strings:" in line:
strings_section = True
# Check if the string condition is on the same line as "strings:"
same_line_match = re.search(r'strings:\s*(\$\w*)\s*=\s*"(.*?)"(?:\s*(fullword|ascii|wide|xor|nocase)?)?', line)
if same_line_match:
variable_name = same_line_match.group(1)
ascii_string = same_line_match.group(2)
# Convert to hex
hex_value = string_to_hex_array(ascii_string)
hex_line = f' {variable_name} = {{{hex_value}}}'
hex_rule += hex_line + "\n"
modifications.append(f"Converted ASCII string on same line to hex: {ascii_string} -> {hex_line.strip()}")
modified = True
else:
hex_rule += line + "\n"
continue
if strings_section:
match = re.search(r'(\$[\w_]+)\s*=\s*("(.*?)"|{([0-9A-Fa-f\s\[\]\?\-]+)})\s*(fullword|ascii|wide|xor|nocase)?', line)
if match:
variable_name = match.group(1)
ascii_string = match.group(3)
hex_array = match.group(4)
modifiers = match.group(5) or ""
if ascii_string:
# Convert ASCII string to hex array
hex_value = string_to_hex_array(ascii_string)
hex_line = f' {variable_name} = {{{hex_value}}}'
hex_rule += hex_line + "\n"
modifications.append(f"Converted ASCII string to hex: {ascii_string} -> {hex_line.strip()}")
modified = True
elif hex_array:
# Keep hex array unchanged
hex_rule += line + "\n"
else:
# Handle single dollar string conditions
single_dollar_match = re.search(r'\$\s*=\s*"(.*?)"', line)
if single_dollar_match:
ascii_string = single_dollar_match.group(1)
hex_value = string_to_hex_array(ascii_string)
hex_line = f' $hex_string = {{{hex_value}}}'
hex_rule += hex_line + "\n"
modifications.append(f"Hex-encoded single $ string: {ascii_string} -> {hex_line.strip()}")
modified = True
else:
hex_rule += line + "\n"
else:
hex_rule += line + "\n"
return hex_rule, rule_name, modifications
def process_file(input_file, output_file, strip_comments=True):
try:
with open(input_file, 'r', encoding='utf-8') as infile:
original_yara_rule = infile.read()
except UnicodeDecodeError:
with open(input_file, 'r', encoding='ISO-8859-1') as infile:
original_yara_rule = infile.read()
converted_yara_rule, rule_name, modifications = process_yara_rule(original_yara_rule, strip_comments=strip_comments)
if modifications:
print(f"Modifications in rule: {rule_name}")
for mod in modifications:
print(f" - {mod}")
with open(output_file, 'w', encoding='utf-8') as outfile:
outfile.write(converted_yara_rule)
def traverse_and_process(input_folder, output_prefix=None, strip_comments=True):
for root, _, files in os.walk(input_folder):
for file in files:
if file.endswith(".yar") or file.endswith(".yara"):
input_file_path = os.path.join(root, file)
if output_prefix:
relative_path = os.path.relpath(input_file_path, input_folder)
output_file_path = os.path.join(root, output_prefix + relative_path)
os.makedirs(os.path.dirname(output_file_path), exist_ok=True)
else:
output_file_path = input_file_path
process_file(input_file_path, output_file_path, strip_comments)
def delete_files_in_yara_folder(root_dir):
# Walk through the directory tree
for root, dirs, files in os.walk(root_dir):
# Check if 'yara' is in the path
if 'yara' in root.lower():
for file in files:
# Check for specific file extensions (unneeded artefacts)
if file.endswith(('.eml', '.csv', '.txt', '.js')):
file_path = os.path.join(root, file)
try:
os.remove(file_path)
print(f"Deleted: {file_path}")
except Exception as e:
print(f"Failed to delete {file_path}: {e}")
def main():
parser = argparse.ArgumentParser(description="Clean YARA rules to avoid AV detection by converting ASCII strings to hex arrays and stripping comments, deleting unneeded artefacts (optional, enabled by default).")
parser.add_argument("input_folder", help="Path to the input folder containing YARA rule files.")
parser.add_argument("--output-prefix", help="Optional prefix for output files. If not provided, original files are overwritten.", default=None)
parser.add_argument("--strip-comments", action="store_true", help="Strip comments from the entire rule (default: True).", default=True)
parser.add_argument("--delete-unneeded-artefacts", dest="delete_artefacts", action="store_true", default=True,
help="Delete .eml, .csv, and .txt files in folders containing 'yara'. Default is True.")
parser.add_argument("--keep-unneeded-artefacts", dest="delete_artefacts", action="store_false",
help="Do not delete .eml, .csv, and .txt files even if folders contain 'yara'.")
args = parser.parse_args()
traverse_and_process(args.input_folder, output_prefix=args.output_prefix, strip_comments=args.strip_comments)
if args.delete_artefacts:
delete_files_in_yara_folder(args.input_folder)
if __name__ == "__main__":
main()

**After-installation troubleshooting**

In some rare cases, you can bump into the following issues after installing Sandbox on a hardened operating system:

`Caused by: java.io.IOException: Error initiating config file: can not write to /app/broker.cfg`

`Caused by: java.io.IOException: Error initiating config file: can not write to /app/transform.cfg`

`nginx: [emerg] cannot load certificate "/etc/ssl/certs/nginx-selfsigned.crt": BIO`*new*`file() failed (SSL: error:80000002:systemlibrary::No such file or directory:calling fopen(/etc/ssl/certs/nginx-selfsigned.crt, r) error:10000080:BIO routines::no such file)`

If you encounter any of those, you should apply the fix below.

Info

You must have Sandbox installed to run the code below.

Warning

In case you installed Sandbox in **OFFLINE** mode, you will need an extra `--offline` flag when you execute the script.

1. Copy the `hardened-install-fix.sh` script below on your sandbox installation path. By default, it is `/home/sandbox/sandbox`
2. Stop Sandbox services using `sudo service sandbox stop`
3. Make the script executable by executing `sudo chmod +x hardened-install-fix.sh`
4. Execute the script by using either `sudo ./hardened-install-fix.sh` or `sudo ./hardened-install-fix.sh --offline` depending, whether the initial install you made was using the offline flag or not.
5. Start Sandbox services by executing `sudo service sandbox start`

hardened-install-fix.shCopy#!/bin/bash
DIR="$(dirname "$(realpath "${0}")")"
OFFLINE_INSTALL=false
if [ "$(id -u)" -ne 0 ]; then
echo "Please run this script as root!"
exit 126
fi
while [ "$#" -gt 0 ]; do
option="$1"
shift
case "$option" in
-h|--help)
USAGE
;;
-v|--verbose)
set -o xtrace
VERBOSE="-v"
;;
--offline)
OFFLINE_INSTALL=true
;;
*)
echo "$0: Invalid argument.. $1" >&2
USAGE
exit 1
;;
esac
done
commandOutput() {
# Column number to place the status message
# Get only without nested/child shells
if [[ $SHLVL -le 2 ]]; then termColumns=$(tput cols); fi
messageColumn=$((termColumns-20))
# Command to move out to the configured column number
moveToColumn="echo -en \\033[${messageColumn}G"
# Command to set the color to SUCCESS (Green)
setColorSuccess="echo -en \\033[32m"
# Command to set the color to FAILED (Red)
setColorFailure="echo -en \\033[31m"
# Command to set the color back to normal
setColorNormal="echo -en \\033[0;39m"
}
success() {
echo -n "["
$setColorSuccess
echo -n $" OK "
$setColorNormal
echo -n "] "
echo -e "$1"
}
error() {
echo -n "["
$setColorFailure
echo -n $"ERROR"
$setColorNormal
echo -n "] "
echo -e "$1"
}
fatal() {
echo -n "["
$setColorFailure
echo -n $"FATAL"
$setColorNormal
echo -n "] "
echo -e "$1"
echo "Exiting..."
exit 1
}
conf() {
if source "$DIR"/install.cfg; then
success "Loaded config from $DIR/install.cfg"
else
fatal "Failed to read the install.cfg file from $DIR."
fi
if source "$DIR"/version.cfg; then
success "Loaded config from $DIR/version.cfg"
else
fatal "Failed to read the version.cfg file from $DIR."
fi
}
stopSandboxService() {
if service --status-all | grep -Fwq 'sandbox'; then
stopSystemService 'sandbox'
# The service might have been inactive, call stop_sandbox.sh just in case
if [[ -f "$Sandbox_Directory"/stop_sandbox.sh ]] && [[ -f '/usr/bin/docker' ]]; then
echo "Stopping sandbox service..."
if "$Sandbox_Directory"/stop_sandbox.sh; then
success "Successfully stopped sandbox service"
else
error "Failed to stop sandbox service"
fi
fi
fi
}
fixTransform() {
if [ -f "$Sandbox_Directory/transform.cfg" ]; then
success "transform.cfg exists and is a file"
else
if [ -d "$Sandbox_Directory/transform.cfg" ]; then
error "transform.cfg is a directory, deleting it"
rm -rf "$Sandbox_Directory"/transform.cfg
else
error "transform.cfg does not exist"
fi
if [ -z "$SandboxTransform_APIKeySecret" ]; then
SandboxTransform_APIKeySecret=$(openssl rand -hex 24)
fi
read -r -d '' transform_cfg <<- EOF
apiKey0.secret=$SandboxTransform_APIKeySecret
apiKey0.authlevel=1000
EOF
if echo "$transform_cfg" > "$Sandbox_Directory"/transform.cfg; then
chown "$Sandbox_User":"$Sandbox_User" "$Sandbox_Directory"/transform.cfg
success "Successfully created transform.cfg"
else
fatal "Failed to create $Sandbox_Directory/transform.cfg"
fi
if [ "$OFFLINE_INSTALL" = true ] ; then
# Enable offlineMode by default for offline installations
echo '' >> "$Sandbox_Directory/transform.cfg"
echo 'offlineMode=true' >> "$Sandbox_Directory/transform.cfg"
fi
fi
echo "transform.cfg permissions:"
namei -l "$(realpath "$Sandbox_Directory"/transform.cfg)"
echo ""
}
fixBroker() {
if [ -f "$Sandbox_Directory/broker.cfg" ]; then
success "broker.cfg exists and is a file"
else
if [ -d "$Sandbox_Directory/broker.cfg" ]; then
error "broker.cfg is a directory, deleting it"
rm -rf "$Sandbox_Directory"/broker.cfg
else
error "broker.cfg does not exist"
fi
if [ -z "$SandboxBroker_APIKeySecret" ]; then
SandboxBroker_APIKeySecret=$(openssl rand -hex 24)
fi
read -r -d '' broker_cfg <<- EOF
apiKey0.secret=$SandboxBroker_APIKeySecret
apiKey0.authlevel=1000
app1.secret=$SandboxTransform_APIKeySecret
EOF
if echo "$broker_cfg" > "$Sandbox_Directory"/broker.cfg; then
chown "$Sandbox_User":"$Sandbox_User" "$Sandbox_Directory"/broker.cfg
success "Successfully created broker.cfg"
else
fatal "Failed to create $Sandbox_Directory/broker.cfg"
fi
fi
echo "broker.cfg permissions:"
namei -l "$(realpath "$Sandbox_Directory"/broker.cfg)"
echo ""
}
fixWebservice() {
selfsigned_key=/etc/ssl/private/nginx-selfsigned.key
selfsigned_crt=/etc/ssl/certs/nginx-selfsigned.crt
dhparam=/etc/ssl/certs/dhparam.pem
if [ -e "$selfsigned_key" ]; then
echo "$selfsigned_key exists, deleting"
rm -rf "$selfsigned_key"
fi
if [ -e "$selfsigned_crt" ]; then
echo "$selfsigned_crt exists, deleting"
rm -rf "$selfsigned_crt"
fi
if [ -e "$dhparam" ]; then
echo "$dhparam exists, deleting"
rm -rf "$dhparam"
fi
if openssl req -x509 -nodes -days 1825 -newkey rsa:2048 \
-subj "/C=DE/ST=Hamburg/L=Germany /O=OPSWAT Inc./OU=Development/CN=*/emailAddress=support@filescan.io" \
-keyout /etc/ssl/private/nginx-selfsigned.key \
-out /etc/ssl/certs/nginx-selfsigned.crt;
then
success "Successfully created self-signed certificate"
else
fatal "Failed to create self-signed certificate"
fi
echo "Creating new DH Parameters (Safe Key Exchange)..."
if openssl dhparam -out "$dhparam" 2048; then
success "Successfully created safe keys"
else
fatal "Failed to create safe keys"
fi
}
commandOutput
conf
stopSandboxService
echo "List of Sandbox installation directory before applying the fix(es):"
ls -lah "$Sandbox_Directory"
if [ "$SandboxTransform_Install" = true ] ; then
fixTransform
fi
if [ "$SandboxBroker_Install" = true ] ; then
fixBroker
fi
if [ "$SandboxWebservice_Install" = true ] ; then
fixWebservice
fi
if chown "$Sandbox_User":"$Sandbox_User" "$Sandbox_Directory"/*.cfg "$Sandbox_Directory"/*.yaml; then
success "Successfully updated config ownership"
else
error "Failed to change config ownership to $Sandbox_User:$Sandbox_User."
fi
echo "List of Sandbox installation directory after applying the fix(es):"
ls -lah "$Sandbox_Directory"
echo "Finished applying the fix(es), please start the Sandbox service manually!"

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

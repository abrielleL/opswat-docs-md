<!-- source: https://www.opswat.com/docs/mdcore/utilities-engines/integrate-with-external-command-line-tools -->

# Integrate with external command line tools

This feature enables users to integrate their own tools with the Archive Extraction engine to extract or decrypt files, allowing them to be further processed by other engines.

**Preparation**:

A JSON file is required to define which tools to use and how to execute them. The root of this JSON should be an array, where each element is a JSON object containing the following mandatory fields:

- `"file_type_id"`: Specifies the target file type.
- `"executable_path"`: The absolute path to the executable tool.
- `"arguments"`: Command-line arguments to run the tool. This must include the `$input` and `$output` placeholders. The `$password` placeholder is optional.
- `"patterns_indicating_encrypted"`: A list of substring in the command-line output that signifies an extraction failure caused by an incorrect password.

Example:

JsonCopy[
{
"file_type_id": "OPENSSL-SALT",
"executable_path": "/usr/bin/openssl",
"arguments": [
"enc",
"-d",
"-des-ebc",
"-in",
"$input",
"-out",
"$output",
"-k",
"$password"
],
"patterns_indicating_encrypted": ["bad decrypt","bad password read"]
},
{
"file_type_id": "OPENSSL-SALT",
"executable_path": "/usr/bin/openssl",
"arguments": [
"enc",
"-d",
"-des3",
"-in",
"$input",
"-out",
"$output",
"-k",
"$password"
],
"patterns_indicating_encrypted": ["bad decrypt","bad password read"]
}
]

**Enable the feature** in Inventory > Modules > Archive extraction > Enable CLI Processing and configure the file path to point to the JSON file.

**To apply the changes, disable and then re-enable the Archive Extraction module.** Modifying the JSON file also requires restarting the engine.

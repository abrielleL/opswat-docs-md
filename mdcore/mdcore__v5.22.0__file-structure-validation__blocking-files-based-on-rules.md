<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/file-structure-validation/blocking-files-based-on-rules -->

# Blocking files based on rules

All blocking rules are off by default, with no rules enabled, FSV only reports what it finds. FSV supports two rule types,

- **Built-in rules**: block on invalid file structure, or on the presence of an object class such as macros, scripts, or embedded objects. These are toggled per workflow.

- **Custom rules**: block on a condition matched against an extracted object's attributes.

  For example, block any PDF file whose embedded hyperlink points to `http://malicious.example`.

  | JSON Path | Value Pattern |
  | --- | --- |
  | $.details[?(@.object_name=="hyperlink")].object_details[*] | http://malicious.example |

<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder -->

# How is the OPC-DA file structured for importing tags with folders?

This article applies to MetaDefender Optical Diode / NetWall Diode.

## [Overview](/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder#overview)

This page explains how to structure a file for importing OPC-DA tags, including how folders and tags are defined within a single import file.

---

## [Key Concepts](/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder#key-concepts)

### [1. Single File, Multiple Folders](/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder#1-single-file-multiple-folders)

- You do *not* need to import folders separately.
- A single file can define and load *multiple folders*.
- Each folder is declared using a special directive.

---

### [2. Folder Definition (`#folder`)](/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder#2-folder-definition-folder)

The `#folder` directive defines where tags will be organized.

*Format:*

#folder,<top folder>,<sub folder>

*Notes:*

- Values are separated by *commas*.
- Both top-level and sub-folder must be provided.

---

### [3. Tag Assignment](/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder#3-tag-assignment)

- All lines following a `#folder` definition belong to that folder.
- Tags use *dot notation*, not commas.

*Format:*

<FolderName>.<TagName>

---

### [4. File Format Clarification](/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder#4-file-format-clarification)

{info:title=Important} Although the file resembles a CSV, it may not look like a typical one.

- The separator is a *comma (,)* — not a space.
- Tag lines themselves do *not* use commas. {info}

---

## [Example File Structure](/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder#example-file-structure)

#folder,Simulation Items,Bucket Brigade
Bucket Brigade.Boolean
Bucket Brigade.Int2
#folder,Simulation Items,Saw-toothed Waves
Saw-toothed Waves.Int1
Saw-toothed Waves.Int2

---

## [How It Works](/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder#how-it-works)

The system reads the #folder line.

All following tag entries are assigned to that folder.

When a new #folder appears, subsequent tags are assigned to the new folder.

---

## [Best Practices](/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder#best-practices)

- Always define folders *before* listing tags.
- Keep naming consistent between folder names and tag prefixes.
- Avoid unintended extra spaces.
- Ensure correct comma placement in `#folder` lines.

---

## [Common Pitfalls](/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder#common-pitfalls)

|| Issue || Explanation || | Using spaces instead of commas | Breaks folder parsing | | Using commas in tag lines | Invalid format | | Missing `#folder` before tags | Tags may not be assigned correctly | | Inconsistent naming | Causes mismatched folder/tag mapping |

---

## [Summary](/docs/netwalldiode/v1.14.0/knowledge-base/how-is-the-opc-da-file-structured-for-importing-tags-with-folder#summary)

{panel:title=Quick Summary}

- Use `#folder` to define folder structure
- Use *comma-separated values* only for folder definitions
- Use *dot notation* for tags
- Multiple folders can be handled in a single import file {panel}

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).

MetaDefender

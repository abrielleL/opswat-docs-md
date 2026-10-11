<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/supported-packers-for-unpacking -->

# Supported packers for unpacking

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Our engine can unpack a wide range of packers, both specific and generic. This is important because packers are often used by malware to evade detection. By unpacking them, we can analyze and identify any embedded threats.

**Specifically supported packers:**

- ASPack,
- FSG,
- MEW,
- MPRESS,
- PEiTe,
- UPX,
- YZPack.

The screenshot from the linked analysis shows the unpacked PE is available for download.

Unpacking

You can find the sample from the screenshot below at the following link:

<https://www.filescan.io/uploads/6502117c9bae8a378555f25f/reports/a50dfc89-c1e4-4dfc-8721-f7c151c14d5f/files>

The screenshot from the linked analysis shows the unpacked PE is available for download.

Additionally, we also support extraction and decompilation of scripting code that has be wrapped as an executable. This technique is commonly found in malware and can be effective to deviate the focus of the analysis from the relevant payload. Hence we detect, extract, and decompile such implementation in order to be able to focus on the relevant payload.

**Supported compiled scripting languages:**

- PyInstaller
- Py2Exe
- Nuitka
- AutoIT
- JPHP

Compiled script unpacking

On the following link you can find the sample from the screenshot below:

[https://www.filescan.io/uploads/66fbacc03aaac9834b817ad2/reports/7418f790-69ae-4366-9e90-7a85cf02cdef/files](https://www.filescan.io/uploads/6502117c9bae8a378555f25f/reports/a50dfc89-c1e4-4dfc-8721-f7c151c14d5f/files)

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/pe-emulator--beta- -->

# Advanced PE emulator (Beta)

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Our custom Windows Portable Executable (EXE) emulator adds high value by reaching unpacking dynamic payloads, hidden IOCs, therefore this feature enables many additional improvements and covers many gaps.

`Note: Currently, the PE emulator is only available for 32-bit native Portable Executable (PE) files. Therefore the emulator excludes 64-bit native PEs and 32-bit/64-bit .NET PEs due to their internal nature (.NET PEs are executed through the .NET framework instead of natively by the OS).`

Additionally, the emulator brings the option to **emulate raw shellcode** by uploading a raw binary shellcode to the sandbox using the `.shellc` extension.

## [Emulator output](/docs/filescan/3.2.0/datasheet/pe-emulator--beta-#emulator-output)

The emulator has 5 types of output files, which are processed by the sandbox. While they are not directly intended to be manipulated by the users, all of them are **available through the UI for further inspection**.

- `out.json` : Contains the emulation events that are implemented, including the event details.
- `api_log.json` : This is an API call trace for the emulation. It includes the API call with the corresponding parameters that were used as arguments for the logged call. The APIs that will be logged are configurable by the user, otherwise the default set will be used.
- `symbols.json` : Contains the mapping of the imported APIs with the corresponding virtual addresses. Includes the dynamically loaded Libraries and APIs, which are not included in the import table.
- `stdout`: Contains the output that the sample execution would send through the standard output, if any.
- `<memory dumps>` : Under specific conditions, the PE emulator will dump files from the process memory, to retrieve dynamic content. These files will be named using a FUID.

## [Emulation events](/docs/filescan/3.2.0/datasheet/pe-emulator--beta-#emulation-events)

Note that while the emulator has already demonstrated high value in its currents status (beta) the implemented events are limited. Currently, the following events that are part of the output are the following, clustered in the corresponding categories:

**File:**

- `Create File` : Writing a binary file to disk.
- `Write Text File` : Writing a text file to disk.

**Network:**

- `Dns Lookup` : Performing a DNS lookup for a given domain.
- `Connect Network` : Establish a connection with a remote host.
- `Http Request` : Perform an HTTP request to a given URL.
- `Receive Network Data` : Read the received network response (currently fake response, no real connection with the remote host).

**Execution:**

- `Tls Callback` : Execute TLS callback functions (code before the PE entry point).
- `Section Hop` : The execution jumps to a memory segment out of the current PE section.

**Memory:**

- `Write Process Memory` : Write content within the memory of a process.
- `Process Struct Access` : Access the current process structure (PIB/TIB).
- `Executable Region` : Assign a memory region execution rights.

**General Events**:

- `Load Library` : Dynamically load a library.
- `Unhandled API` : API function which the emulator does not support.
- `Exception` : An exception occurring on the emulated process.
- `LocateAPI` : Dynamically locate the address of a Windows API function.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

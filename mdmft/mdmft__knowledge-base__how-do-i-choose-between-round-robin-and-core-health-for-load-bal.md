<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-do-i-choose-between-round-robin-and-core-health-for-load-bal -->

# How Do I Choose Between Round Robin and Core Health for Load Balancing Multiple MetaDefender Cores in MFT?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article applies to MetaDefender Managed File Transfer version 3.10.2 and later, the release in which the Core Health (Smart Routing) load balancing option was introduced.

**Terminology note:** The load-aware mode is labelled Core Health in the MFT documentation and UI. Internally it is also referred to as Smart Routing (the term that appears in the processor logs). Both names describe the same feature.

When MetaDefender Managed File Transfer (MFT) is integrated with more than one MetaDefender Core, MFT distributes scanning requests across the Cores using a selectable load balancing method. This article explains the two available modes — Round Robin and Core Health — how each behaves and the use cases each is suited to.

The load balancing method is a single global setting applied to every file transferred. MFT does not route individual files based on their size or type — the mode you select governs how all files are distributed. The use-case guidance below is therefore about choosing the mode that best fits your typical workload, not about per-file routing.

**Round Robin**

Round Robin distributes files evenly across all configured Cores in a fixed rotating sequence (Core A → Core B → Core C → Core A …). Every Core is utilized in turn.

- How it works: each incoming file is sent to the next Core in the rotation, regardless of how busy each Core currently is.
- Recommended use cases: small files such as Word documents and PDFs, where scan times are short and predictable.

**Core Health (Smart Routing)**

Core Health routes each file to the healthiest Core — the one with the most capacity to take on more files — rather than following a fixed rotation. The healthiest Core is fully utilized first.

- How it works: MFT triggers an API call to check each Core's status and selects the Core with the lowest current CPU load. "Health" is determined purely by current CPU load — queue depth and scan-duration data are not factored in. Unhealthy Cores are automatically skipped. The processor log records each Smart Routing decision, including the CPU% used to select the Core.
- Recommended use cases: large files, or archived files containing many small files, where scan durations are longer and uneven.
- The load-aware distribution avoids stacking heavy files onto a Core that is already busy, improving throughput for large or uneven workloads.

**Storage Handling for Large Files (applies to both modes)**

The following behavior applies regardless of which load balancing mode is selected:

- If a large file exceeds the available space on the Cores, that file must wait until enough storage space is freed up before it can be transferred and scanned.
- In the meantime, other smaller files will continue to be transferred and scanned as space permits — they are not blocked by the waiting large file.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

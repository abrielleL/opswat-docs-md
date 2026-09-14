<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown -->

# Preventing SDK Process-Exit Crashes with proper Teardown

A short, intermittent class of process-exit crashes traces back to OESIS Framework being shut down by the operating system instead of by your application. This advisory explains the recommended pattern, why it matters, what the impact is, and how to confirm the fix.

Recommendation at a glance

Always shut the SDK down explicitly (using `wa_api_teardown()` before your process ends:

- Call `wa_api_teardown()`**before your process begins to terminate**, on a normal, healthy code path.
- Call it from the **same thread that called** `wa_api_setup()`.
- **Never** call it from `atexit`, `DllMain` (Windows), a signal handler, an `abort()` path, or anything else that runs *while the process is already exiting*.

Doing all of these removes a class of intermittent process-exit crashes whose root cause is the SDK being shut down by the operating system instead of by your application.

## [Who this applies to](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#who-this-applies-to)

This advisory is for any application that embeds the OESIS V4 (the `wa_api_*` C interface). The guidance is the same on Windows, macOS, and Linux; the failure is most visible on Windows, but the underlying rule is cross-platform.

If your integration calls `wa_api_teardown()` on the setup thread before exiting the process, no change is required. This document explains why that pattern is the correct one.

## [The recommendation](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#the-recommendation)

A correct teardown must satisfy **all three** of the following:

### [1. Call wa_api_teardown() before the process starts to exit](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#1-call-wa_api_teardown-before-the-process-starts-to-exit)

`wa_api_teardown()` performs the SDK's **orderly shutdown**: it releases internal memory and handles, finishes or cancels in-flight work, releases external resources, and cleans up any child processes the SDK started - all while the runtime is still healthy and every dependency the SDK relies on is still alive.

The natural place to call it is your application's normal exit path, for example just before returning from your entry point (`main`, or `WinMain` on Windows), or before any deliberate process-exit call (`exit()`, or `ExitProcess()` on Windows).

### [2. Call it from the same thread that called wa_api_setup()](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#2-call-it-from-the-same-thread-that-called-wa_api_setup)

Some of OESIS's state is **per-thread**, not global - thread-local storage, and on Windows the impersonation context and the COM apartment.

Per-thread state can only be released safely from the thread that established it. If teardown runs on a different thread, the setup thread's state is left in place and is only cleaned up later by the operating system during process exit, which is exactly the unsafe situation this advisory is about.

### [3. **Never** tear down from a process-termination path](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#3-never-tear-down-from-a-process-termination-path)

Do not move the call into `atexit`, `DllMain`, a signal handler, an `abort()` handler, or any other code that runs once the process has already begun to exit. By that point the runtime is in a partially torn-down state (on Windows, the operating system also holds the loader lock), which is not a safe environment for the work teardown needs to do.

## [What correct usage looks like](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#what-correct-usage-looks-like)

The lifecycle is symmetric: set up once, use the SDK, then tear down once - on the same thread, before exit. For example:

Correct usageCopyint main(int argc, char** argv)
{
wa_wchar* out = NULL;
if (wa_api_setup(json_in, &json_out) != WAAPI_OK) {
/* handle setup failure */
return 1;
}
wa_api_free(json_out);
/* ...
use the SDK: wa_api_invoke(...), register handlers, etc.
... */
wa_api_teardown();
/* same thread as wa_api_setup(), on the normal exit path */
return 0;
}

And a few patterns to avoid:

during terminationwrong threadfrom DllMainCopy/* WRONG: runs during process termination, not before it */
atexit(wa_api_teardown);/* WRONG: teardown on a worker thread, not the thread that called wa_api_setup() */
std::thread([]{ wa_api_teardown(); }).join();/* WRONG: teardown from a DLL unload notification (Windows) or a signal handler */
BOOL WINAPI DllMain(HINSTANCE h, DWORD reason, LPVOID reserved) {
if (reason == DLL_PROCESS_DETACH) wa_api_teardown(); /* far too late */
return TRUE;
}
## [Why it matters](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#why-it-matters)

If `wa_api_teardown()` is never called, the SDK's internal objects are not released by your application. They survive until the very end of the process, and the C/C++ runtime then destroys them automatically as part of the operating system's process-shutdown sequence.

That automatic, end-of-process cleanup runs in a hostile environment - the process is already terminating, dependencies the SDK objects relied on may already be gone, and (on Windows) the loader lock is held. A cleanup step that is perfectly safe on a normal thread can fault in that environment.

Both paths below lead to the same logical place - the SDK's state being released - but only one runs while it is safe to do so.

Recommended path

1. `wa_api_setup()` on thread T.
2. `wa_api_invoke()` … your work.
3. `wa_api_teardown()` on thread T, before exit → state released cleanly.
4. Process exits, nothing left for the OS to clean up.
Path that crashes

1. `wa_api_setup()` on thread T.
2. `wa_api_invoke()` … your work.
3. Process exits with no teardown.
4. The runtime destroys SDK objects during shutdown, cleanup touches already-torn-down state → crash.
## [What you will see if teardown is skipped](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#what-you-will-see-if-teardown-is-skipped)

The characteristic symptom is a crash **at process exit**, not during your application's normal work:

- On **Windows**, an access violation (`0xC0000005`) faulting inside an OESIS SDK module, with a call stack that shows the process already shutting down, the runtime running static-object destructors from inside the loader's DLL-detach (`DLL_PROCESS_DETACH`) sequence, rather than from an explicit teardown call.
- On **macOS and Linux**, a crash or abort during the equivalent end-of-process static-destructor phase.

Beyond the crash itself, skipping the orderly shutdown can also leave work unfinished that teardown would normally complete: external resources not released, debug logs not fully flushed, and child processes the SDK started left orphaned.

Warning

The crash happens ***after*** your application's useful work is done, so it can look harmless — but it still produces crash dumps, can trigger Windows Error Reporting or host watchdogs, and signals that the SDK never got to shut down cleanly. The fix is the same in every case: call `wa_api_teardown()` correctly.

## [Why the crash is intermittent (and why “it works on my machine” is misleading)](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#why-the-crash-is-intermittent-and-why-it-works-on-my-machine-is-misleading)

The same missing-teardown integration can crash on one run and complete cleanly on the next, and a build that appeared fine yesterday can crash today with no code change. That is because whether the end-of-process cleanup happens to touch already-released memory depends on factors that are not under your application's control:

| Factor | Why it varies the outcome |
| --- | --- |
| Operating-system version, build, and patch level | The OS shutdown sequence and the timing of thread-local, heap, and handle cleanup differ between builds. The same binary can crash on one OS build and not another. |
| Per-run memory layout | Heap state, address-space layout, and allocator fragmentation differ every run. Reading a just-freed object can succeed if its bytes have not been reused yet, and fault if they have. |
| SDK build internals | The order in which the runtime destroys static objects is fixed when the SDK is compiled and can shift between SDK releases (compiler, optimization, link order) with no behavior change — so the same issue can be visible in one SDK build and silent in another. |
| State of dependencies at unload | Some SDK objects own external resources whose state at shutdown depends on timing, machine speed, and system load. One run takes a short, safe cleanup path; another takes a longer path into something already torn down. |

None of these are reliably controllable by you or by us — the operating system owns most of them. The single thing that *is under your control* is whether the SDK gets to shut down on a healthy thread before the process exits. Calling `wa_api_teardown()` correctly removes all of the above from the equation at once.

## [How to apply this](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#how-to-apply-this)

- Call `wa_api_teardown()` exactly once, on the same thread that called `wa_api_setup()`, on your normal exit path.
- Make sure that thread is still alive at shutdown time, if you set the SDK up on a dedicated thread, tear it down on that same thread before the thread ends.
- Remove any `wa_api_teardown()` call registered with `atexit`, or placed in `DllMain`, a signal handler, or an `abort()` path.
- Let `wa_api_teardown()` return before the process proceeds to exit normally.

## [How to confirm it is correct](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#how-to-confirm-it-is-correct)

You can verify the fix without any internal tooling:

- **Debug logs:** with SDK debug logging enabled, a clean run shows `wa_api_teardown` being entered (and returning) on the setup thread, near the end of the run.
- **Crash dumps:** after the change, you should no longer see crash dumps whose faulting stack shows SDK destructors running from the operating system's process-shutdown / DLL-detach path. If a dump still shows that pattern, teardown is either not being called or is being called too late.

## [Frequently asked questions](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#frequently-asked-questions)

**Our application only exits when the machine shuts down, do we still need this?**

- Yes. Process exit is process exit, whether it is triggered by your code, by the user, or by the OS asking the process to close. The orderly shutdown should run on a healthy thread before that exit begins.

**We never saw a crash. Does that mean we are fine?**

- Not necessarily. The crash is intermittent by nature (see [the factors](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#why-the-crash-is-intermittent-and-why-it-works-on-my-machine-is-misleading) above). The correct test is whether `wa_api_teardown()` is called on the setup thread before exit, not whether a crash has been observed.

**Can we just call** **wa_api_teardown()** **from any thread to be safe?**

- No. Some SDK state is per-thread and can only be released from the thread that created it. Tearing down from a different thread leaves that state for the OS to clean up at process exit - the situation this advisory exists to prevent.

**What does** **wa_api_teardown()** **return, and should we check it?**

- It returns `WAAPI_OK` on success and an error code otherwise (including if `wa_api_setup()` was never successfully called). Checking the return value is good practice, but the key point of this advisory is *when* and *on which thread* you call it.

## [Glossary](/docs/mdsdk/knowledge-base/preventing-sdk-process-exit-crashes-with-proper-teardown#glossary)

- **wa_api_setup**: OESIS lifecycle entry point. Initializes the framework; must be paired with a later `wa_api_teardown()` on the same thread.
- **wa_api_teardown**: OESIS lifecycle exit point. Releases all internal state in an orderly way; must be called on the setup thread, before the process begins to terminate.
- **wa_api_invoke**: OESIS call used to perform detection / management operations between setup and teardown.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

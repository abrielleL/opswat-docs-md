<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/operating/remote-script-execution-from-central-management -->

# Remote Script Execution from Central Management

View as Markdown Ask ChatGPT about this page Ask Claude about this page
# [Remote Script Execution from Central Management](/docs/mdkiosk/v4.8.6/operating/remote-script-execution-from-central-management#remote-script-execution-from-central-management)

If you manage your MetaDefender Kiosk devices with Central Management, you can run a custom script on one or many Kiosks remotely, without visiting each device. This is useful for fleets in air-gapped, restricted-network, or large-scale environments where you can only reach Central Management directly — for example, to run a one-off maintenance task or collect a diagnostic file across many Kiosks at once. Available starting in Kiosk 4.8.3.

## [Prerequisites](/docs/mdkiosk/v4.8.6/operating/remote-script-execution-from-central-management#prerequisites)

- The Kiosk must be enrolled and managed by Central Management. Standalone Kiosks that are not enrolled cannot receive remote scripts.
- MetaDefender Kiosk 4.8.3 or later must be installed on the device.
- The script must be a batch script (a `.bat`-style command script). Other script types, such as PowerShell, are not supported yet.

## [Running a Script from Central Management](/docs/mdkiosk/v4.8.6/operating/remote-script-execution-from-central-management#running-a-script-from-central-management)

1. In Central Management, open **Inventory**, then select **Script**.
2. Create a new script job and enter the batch script you want to run.
3. Set a timeout — the maximum time the script is allowed to run before it's automatically stopped.
4. Select one or more Kiosk instances to target.
5. Optionally, choose a scheduled time for the job instead of running it right away.
6. Confirm the job. Each targeted Kiosk picks up the script the next time it checks in and runs it in the background.
7. Track progress for each targeted Kiosk from the job view, and review its output once the job finishes.

## [Cancelling a Script](/docs/mdkiosk/v4.8.6/operating/remote-script-execution-from-central-management#cancelling-a-script)

1. Open the script job in Central Management.
2. Choose **Cancel** for one or more targeted Kiosks.
3. Depending on where each Kiosk is in the process, it either skips a script that hasn't started yet, stops a script that's currently running, or — if the script already finished — simply reports its final result with no further action.

### [What you'll see while a job runs](/docs/mdkiosk/v4.8.6/operating/remote-script-execution-from-central-management#what-youll-see-while-a-job-runs)

Each targeted Kiosk reports its own status as the job progresses — for example, waiting to start, running, and then a final **succeeded** or **failed** result. Central Management shows this status per Kiosk, so with a job targeting many devices you can see which ones have finished and which are still in progress. A failure on one Kiosk does not affect the others.

Note

The final result reported for a script is a simple succeeded/failed status — Central Management does not report the script's specific exit code.

## [Example: Running a diagnostic script across a fleet](/docs/mdkiosk/v4.8.6/operating/remote-script-execution-from-central-management#example-running-a-diagnostic-script-across-a-fleet)

An administrator wants to collect a log file from every Kiosk at a remote site:

1. In **Inventory → Script**, the administrator creates a job with a batch script that copies the relevant log file to a shared location, sets a 10-minute timeout, and selects all Kiosks at that site.
2. Each Kiosk runs the script in the background — normal scanning and the Kiosk's on-screen interface are unaffected.
3. As each Kiosk finishes, it reports **succeeded** and its output becomes available in the job view.
4. If a particular Kiosk is offline when the job is dispatched, it picks up and runs the script the next time it reconnects.

Note

Only one script runs on a given Kiosk at a time. If you dispatch several script jobs to the same Kiosk close together, they run one after another rather than at the same time.

Note

Avoid scripts that wait for keyboard input (for example, a script that pauses for a keypress). Since there's no keyboard attached to a remote Kiosk during script execution, a script like this will simply run until the timeout ends it. Give scripts a timeout that comfortably covers how long they're expected to take, and avoid interactive prompts.

Note

Keep a script's output reasonably sized. Scripts that produce very large amounts of output can slow down or interfere with result reporting.

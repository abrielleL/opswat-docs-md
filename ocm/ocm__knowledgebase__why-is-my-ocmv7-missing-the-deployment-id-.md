<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/why-is-my-ocmv7-missing-the-deployment-id- -->

# Why is my OCMv7 missing the Deployment ID?

OCM relies on runtime components from the Microsoft **Visual C++ 2013 Redistributable (x64)**. If these libraries are not present—or are an earlier build—the component that renders the Deployment ID cannot load, leaving the field empty.

- Required package: **Visual C++ Redistributable Packages for Visual Studio 2013 (x64)**
- Required version (minimum): **12.0.40664** (released April 2022)

**Resolution**

1. **Download the redistributable**

   1. Official Microsoft page: search for "Visual C++ Redistributable Packages for Visual Studio latest version".
   2. Direct download (64‑bit): <https://aka.ms/highdpimfc2013x64enu>
2. **Install the package**

   1. Run vcredist_x64.exe and follow the on‑screen prompts.
   2. A reboot is not usually required, but one is recommended if prompted.
3. **Restart OPSWAT services**

   1. Open **Services.msc**. Restart **OPSWAT Central Manager Service** (or restart the server during the optional reboot).
   2. Restart **OPSWAT Central Manager Service** by right-clicking the tray Icon and select Restart
4. **Verify**

   1. Log back in to OCM.
   2. Navigate to **Dashboard › License** and confirm that the **Deployment ID** now appears.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-windows-update--agent-shows-up-to-date-but-my-opswat-cent -->

# How do Windows update "agent shows up-to-date but My OPSWAT Central Management still shows OS missing" patches work?

In some situations, we can see a difference between Windows Update Agent (WUA) and My OPSWAT Central Management. Microsoft has a scheduler to update the WUA UI. They are not constantly run because it will affect to performance of the device. This happens because it's not time to run a schedule of the WUA UI yet.

We can check the issue by using the OPSWAT script to get all OS missing patches on the device. The script result will return all missing patches in real time

GitHub: https://github.com/nguyenmanhhung2611/os-missing-patches/blob/main/GetMissingPatches_WindowsUpdate.vbs

The output result will show the same as the current folder script. You can custom the path here

```bash
outFile="GetMissingPatchesLogs.txt"
```

You also can use another OPSWAT script to manually install OS patches. Runs the script as an administrator

GitHub: https://github.com/nguyenmanhhung2611/os-missing-patches/blob/main/InstallMissingPatches_WindowsUpdate.vbs

Get the KB title via the output of the script to get the missing pa

tches above

![](https://uploads.developerhub.io/prod/97qW/uivdw1e1919kh3gjhhmcthux3p9x8lgvn5dx02rn1xqfg0rzd7p4x4searx0jhqi.png)

Input the KB title to the install missing patches script

```bash
updateTitle = "Dell Inc. - Monitor - 1/7/2016 12:00:00 AM - 1.0.0.0"
```

> **Support:**
>
> For further queries or concerns regarding the **Windows update agent shows up-to-date but** **My OPSWAT Central Management still shows OS missing patches**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s)

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)

<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/why-is-real-time-processing-not-detecting-new-files-on-an-smb-sh -->

# Why is Real Time Processing not detecting new files on an SMB share?

> **Check your version:**
>
> This article applies to all MetaDefender Storage Security releases deployed on Windows or Linux systems.

## **Overview**

Real Time Processing (RTP) on SMB shares is designed to automatically detect and scan new files as they arrive on the share. In some environments, files copied into the share are never picked up by RTP, even though On Demand and Scheduled scans against the same share work correctly and the logs show no errors. This article explains why this happens and how to configure MetaDefender Storage Security to detect these files.

## **Cause**

Polling based RTP on SMB shares detects new files by their **LastModifiedDate**, not by the time they arrive on the share. Most copy tools preserve a file's original modified timestamp during a copy, so a copied file whose modified date is older than the job's discovery start date is never classified as new and is never picked up, even though On Demand and Scheduled scans find it since they enumerate the entire share. No errors appear in the logs because nothing is failing, the file is simply not considered new.

You can check a file's modified date as follows:

- **Windows:** In File Explorer, right-click the file, select **Properties**, and check the **Modified** date on the General tab. You can also view the **Date modified** column directly in File Explorer.

![](https://media-cdn.atlassian.com/file/2f2cf6a8-156d-4f8b-8d07-00945ce89aba/image/cdn?allowAnimated=true&client=b47ea4f6-8f9b-4bc9-91fb-0fbb2816d9aa&collection=contentId-5593006136&height=125&max-age=2592000&mode=full-fit&source=mediaCard&token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJiNDdlYTRmNi04ZjliLTRiYzktOTFmYi0wZmJiMjgxNmQ5YWEiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpjb2xsZWN0aW9uOmNvbnRlbnRJZC01NTkzMDA2MTM2IjpbInJlYWQiXX0sImV4cCI6MTc5MTI1Nzc3OSwibmJmIjoxNzkxMjU0ODk5LCJhYUlkIjoiNzEyMDIwOmQ2N2Y0MWM2LTYxYzMtNDc4MC04YjU0LTUyYTQ4YzhhN2YzMyIsImh0dHBzOi8vaWQuYXRsYXNzaWFuLmNvbS9hcHBBY2NyZWRpdGVkIjpmYWxzZSwiYXV0aFR5cGUiOiJzZXNzaW9uIn0.pCluvMNMlpMR-5_zrRekv8Qv8RglTacjU5zH6Z7iRJo&width=290#media-blob-url=true&id=2f2cf6a8-156d-4f8b-8d07-00945ce89aba&clientId=b47ea4f6-8f9b-4bc9-91fb-0fbb2816d9aa&contextId=contentId-5593006136&collection=contentId-5593006136)

A file's Modified date shown in the file's Properties on a Windows system

- **Linux:** Run `ls -l <filename>` to see the modification time, or `stat <filename>` and check the **Modify** field for the full timestamp.

![](https://media-cdn.atlassian.com/file/329ca68d-76ad-47f1-b89a-e6fe057029eb/image/cdn?allowAnimated=true&client=b47ea4f6-8f9b-4bc9-91fb-0fbb2816d9aa&collection=contentId-5593006136&height=125&max-age=2592000&mode=full-fit&source=mediaCard&token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJiNDdlYTRmNi04ZjliLTRiYzktOTFmYi0wZmJiMjgxNmQ5YWEiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpjb2xsZWN0aW9uOmNvbnRlbnRJZC01NTkzMDA2MTM2IjpbInJlYWQiXX0sImV4cCI6MTc5MTI1Nzc3OSwibmJmIjoxNzkxMjU0ODk5LCJhYUlkIjoiNzEyMDIwOmQ2N2Y0MWM2LTYxYzMtNDc4MC04YjU0LTUyYTQ4YzhhN2YzMyIsImh0dHBzOi8vaWQuYXRsYXNzaWFuLmNvbS9hcHBBY2NyZWRpdGVkIjpmYWxzZSwiYXV0aFR5cGUiOiJzZXNzaW9uIn0.pCluvMNMlpMR-5_zrRekv8Qv8RglTacjU5zH6Z7iRJo&width=550#media-blob-url=true&id=329ca68d-76ad-47f1-b89a-e6fe057029eb&clientId=b47ea4f6-8f9b-4bc9-91fb-0fbb2816d9aa&contextId=contentId-5593006136&collection=contentId-5593006136)

A file's modified date shown in the output of `ls -l` on Linux.

### **Additional Configuration**

This setting changes how the SMB discovery service handles Real Time Processing so that files are picked up based on their presence on the share rather than their LastModifiedDate. The same configuration line applies to both Windows and Linux deployments. To make RTP detect files on SMB shares regardless of their modified timestamps, add the following line to the `customer.env` file:

`DISCOVERY_SERVICE_SMB_RTP_HANDLING=1`

 

**On Linux:**

1. Open `/etc/mdss/customer.env` in a text editor
2. Add the line above (if the parameter already exists, edit its value)
3. Save the file
4. Restart the application by running the following command in a terminal:

```powershell
sudo mdss -c restart
```

 

**On Windows:**

1. Open `C:\Program Files\OPSWAT\MetaDefender Storage Security\config\customer.env` in a text editor
2. Add the line above (if the parameter already exists, edit its value)
3. Save the file
4. Restart the application by running the following commands in PowerShell as Administrator:

```powershell
cd "C:\Program Files\OPSWAT\MetaDefender Storage Security\scripts"
.\mdss.ps1 -c refresh
```

> **Support:** If you have questions, concerns or want to report issues regarding **MetaDefender** **Storage Security**, please open a [Support Case](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

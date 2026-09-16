<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-unknown-devices-are-randomly-registered-to-metadefender-it-a -->

# Why unknown devices are randomly registered to My OPSWAT Central Management?

> **Check Your Version:**
>
> This article applies to all versions of My OPSWAT Central Management and MetaDefender Endpoint.

Some customers report that unknown devices appear to have been unexpectedly registered in IT Access.

Upon investigation, it was found that these devices were using On-Demand registration.

Our suspicion is that the On-Demand Agent (EXE file) was shared within the organization and subsequently scanned by Microsoft Defender for Office 365 Safe Attachments, which was enabled for SharePoint, OneDrive, or Teams.

After being asynchronously scanned by Microsoft 365’s common virus detection engine, Safe Attachments may have detonated the On-Demand Agent file in a virtual environment. This detonation process could have triggered the temporary registration of those devices in IT Access.

## **Recommendations**

- Verify whether the On-Demand Agent EXE file was shared internally through SharePoint, OneDrive, or Teams.
- Confirm if Safe Attachments is enabled in Microsoft Defender for Office 365 for your environment.
- If this behavior is not expected or desired, OPSWAT recommends reviewing how the On-Demand Agent is distributed within your organization to prevent unnecessary scans or detonation events.
- See the article “How to Manage Unknown Devices That Register Automatically?” for pro-active solution.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

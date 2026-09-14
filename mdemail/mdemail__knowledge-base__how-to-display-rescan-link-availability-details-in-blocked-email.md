<!-- source: https://www.opswat.com/docs/mdemail/knowledge-base/how-to-display-rescan-link-availability-details-in-blocked-email -->

# How to display rescan link availability details in blocked email notifications?

This article applies to all MetaDefender Email Gateway Security V5 and 6 releases deployed on Windows systems.

## [Overview](/docs/mdemail/knowledge-base/how-to-display-rescan-link-availability-details-in-blocked-email#overview)

In older versions of **MetaDefender Email Security**, the *Blocked Email* notification included details about the rescan link availability.

In newer versions, the notification only displays the rescan link itself, without the availability details.

Currently, the rescan link availability details:

- **Can only be configured** under:
- *Advanced Threat Prevention > Handling of the Email (Delete Blocked Contents) > Encrypted Email Disclaimer**
- **Cannot be configured** under:
- *Advanced Threat Prevention > Handling of the Email (Block Email)**

There is no built-in option to configure the display of the rescan URL availability for blocked emails in the UI.

---

## [Workaround: Manually Edit the Notification Template](/docs/mdemail/knowledge-base/how-to-display-rescan-link-availability-details-in-blocked-email#workaround-manually-edit-the-notification-template)

To display the rescan link availability details in blocked email notifications, you must manually edit the `notification_blocked.xsl` file.

### [Default File Location](/docs/mdemail/knowledge-base/how-to-display-rescan-link-availability-details-in-blocked-email#default-file-location)

`C:\Program Files\OPSWAT\MetaDefender Email Security\mailagenthost\xslt\`

---

## [Steps to Configure](/docs/mdemail/knowledge-base/how-to-display-rescan-link-availability-details-in-blocked-email#steps-to-configure)

1. Navigate to the following folder in the Email Security installation directory: `C:\Program Files\OPSWAT\MetaDefender Email Security\mailagenthost\xslt\`
2. Locate the file: `notification_blocked.xsl`
3. Open the file using a text editor such as:

   - Notepad
   - Notepad++
4. Add the required rescan link availability text in the appropriate section of the template.
5. Save the file. The text can be customized according to your requirements.

<xsl:choose>
<xsl:when test="rescan_link_show = '1'">
<p>
<h6>
To initiate a rescan and provide the password(s), click the following link (expires at <xsl:value-of select="rescan_link_expiry_time" />):
<xsl:element name="a">
<xsl:attribute name="href">
<xsl:value-of select="rescan_link_url" />
</xsl:attribute>
<xsl:value-of select="rescan_link_url"/>
</xsl:element>
</h6>
</p>
</xsl:when>
<xsl:when test="org_quarantined = '1'">
<p>
<h6>
The original –potentially harmful– email was put into quarantine. If you think that this email was erroneously blocked, contact your administrator to release it.
</h6>
</p>
</xsl:when>
</xsl:choose>

## [Important Note](/docs/mdemail/knowledge-base/how-to-display-rescan-link-availability-details-in-blocked-email#important-note)

Warning

The `notification_blocked.xsl` file **will be overwritten during product upgrades**.

To prevent losing your customization:

- Back up your modified `notification_blocked.xsl` file before upgrading.
- Restore your customized version or add the customized text after the upgrade is complete.

---

##

- Rescan link availability details are not configurable via the Block Email handling settings.
- Manual modification of `notification_blocked.xsl` is required.
- Always back up the file before performing upgrades.

If you require assistance modifying the XSL template safely, consider testing changes in a non-production environment first.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).

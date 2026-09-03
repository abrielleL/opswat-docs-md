<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/knowledge-base/how-can-we-identify-the-insufficient-memory-issue-encountered-in -->

# How can we identify the Insufficient memory Issue encountered in MetaDefender Email Security

This article applies to version 6.1.1 and 6.0.0 of Metadenfer Email Security deployed on Windows systems.

When the management console of Metadefender Email Security becomes unreachable and emails are not being processed anymore.

Entries like the following in the Metadefender Email Security support package indicate the Insufficient Memory Issues.

[ERROR ] 2025.01.02 10:00:28.674: Inserting email entry failed,
reason='ERROR: unterminated quoted string at or near "'
1�������յ�́M���ɥ�������1��������ɕ́Q���䰀����ļ���ԁٽ���1�����%�ѕ����ѥ����I��耀��ň�ݑ����݈��јՐ�����ل��ݙ����ь���"
LINE 1: ' test@testmail.con', 'testadmin@admin.co, '1�������...
^[ERROR ] 2025.01.02 10:00:28.674: [t10952](common.base) Insufficient memory, terminating, message='bad allocation' [msgid: 2892]

This can be related to the behavior addressed in version 6.1.2 of Metadefender Email Security

### [Troubleshoot](/docs/mdemail/6.4.1/knowledge-base/how-can-we-identify-the-insufficient-memory-issue-encountered-in#troubleshoot)

To troubleshoot this issue, it is only necessary to upgrade the current version of Metadefender Email Security to version 6.1.2 or higher.

After this upgrade process of Metadefender Email Security, the emails will be reprocessed, and normal functionality will be restored.

### [Workaround](/docs/mdemail/6.4.1/knowledge-base/how-can-we-identify-the-insufficient-memory-issue-encountered-in#workaround)

There is a workaround for this behavior, which consists of deleting the *.content* and *.envelope* files inside the folder. :

**C:\Program Files\OPSWAT\MetaDefender Email Security\mailagenthost\in**

Support

If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support-services).

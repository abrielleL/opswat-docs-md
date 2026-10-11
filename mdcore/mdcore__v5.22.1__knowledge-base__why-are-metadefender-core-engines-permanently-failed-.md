<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-are-metadefender-core-engines-permanently-failed- -->

# Why are MetaDefender Core engines permanently failed?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### [**Introduction:**](/docs/mdcore/v5.22.1/knowledge-base/why-are-metadefender-core-engines-permanently-failed-#introduction)

This knowledge base article provides details regarding the Core AV engines

#### [**Details:**](/docs/mdcore/v5.22.1/knowledge-base/why-are-metadefender-core-engines-permanently-failed-#details)

We found that the issue is coming from an environmental activity which deleted the /var/tmp folder after 30 days, thus preventing MD Core's internal tasks to update the engines because the oms_testfile is deleted. We have performed the below steps to resolve the issue:

- we have checked the current configuration of the automatic cleanup task with below command:

`cat usr/lib/tmpfiles.d/tmp.conf`

- We have then proceed with modifying the file using below command:

`sudo vim usr/lib/tmpfiles.d/tmp.conf`

- Inside the config file, we have disabled the following parameters by adding a comment sign "#" in front of them:

`# v /tmp 1777 root root 10d ->` deletes the folder /tmp after 10 days

`# v /vat/tmp 1777 root root 30d ->` deletes the folder /var/tmp after 30 days -> Here MD Core creates it's temporary files and these files and folders should not be deleted during functionality

- after this activity has been completed, save the document, using the command

`:wq`

- We have implemented these changes by restarting the cleanup service using the below command

`systemctl stop systemd-tmpfiles-setup.service systemd-tmpfiles-clean.timer`

`systemctl start systemd-tmpfiles-setup.service systemd-tmpfiles-clean.timer`

Once the above activities have been completed, the cleanup services should not affect MD Core functionality.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

<!-- source: https://www.opswat.com/docs/filescan/3.2.0/faq/why-do-you-receive-error-message--failed-to-prepare-repositories -->

# Why do you receive error message "Failed to prepare repositories"?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info:

This article applies to all Sandbox versions

Issue: While installing the Sandbox, the installer fails at the “prepare repositories” step with:

HtmlCopy......
grub2-tools-extra.x86_64 1:2.06-90.el9
grub2-tools-efi.x86_64 1:2.06-90.el9
libldb.x86_64 2.4.1-1.el9
libldb.x86_64 2.6.1-1.el9
[FAIL] Failed to prepare repositories.
Exiting

Even though the system has internet access and the repos are functional.

### [Cause](/docs/filescan/3.2.0/faq/why-do-you-receive-error-message--failed-to-prepare-repositories#cause)

The script **install.sh** uses `dnf check-update` to verify repositories. However, this command returns:

- `0`: No updates available (success)
- `100`: Updates available (still success)
- `>1`: Real error

The script only treats `0` as success, so it fails when updates are available (`100`).

### [Solution](/docs/filescan/3.2.0/faq/why-do-you-receive-error-message--failed-to-prepare-repositories#solution)

## [**Ensure that you have followed these steps before running the installer:**](/docs/filescan/3.2.0/faq/why-do-you-receive-error-message--failed-to-prepare-repositories#ensure-that-you-have-followed-these-steps-before-running-the-installer)

### [Step 1: Install EPEL (if needed)](/docs/filescan/3.2.0/faq/why-do-you-receive-error-message--failed-to-prepare-repositories#step-1-install-epel-if-needed)

HtmlCopysudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm -y
### [Step 2: (Optional) Create sandbox user](/docs/filescan/3.2.0/faq/why-do-you-receive-error-message--failed-to-prepare-repositories#step-2-optional-create-sandbox-user)

HtmlCopysudo useradd --create-home sandbox
sudo passwd -l sandbox
### [Step 3: Install tools like 7zip](/docs/filescan/3.2.0/faq/why-do-you-receive-error-message--failed-to-prepare-repositories#step-3-install-tools-like-7zip)

HtmlCopysudo dnf update -y
sudo dnf install p7zip -y
## [**(Optional) Fix the script logic to allow both 0 and 100:**](/docs/filescan/3.2.0/faq/why-do-you-receive-error-message--failed-to-prepare-repositories#optional-fix-the-script-logic-to-allow-both-0-and-100)

HtmlCopydnf check-update ${DNF_OPTIONS}
result=$?
if [ "$result" -eq 0 ] || [ "$result" -eq 100 ]; then
success "Successfully prepared repositories"
else
fatal "Failed to prepare repositories."
fi
## [Result:](/docs/filescan/3.2.0/faq/why-do-you-receive-error-message--failed-to-prepare-repositories#result)

Support:

If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

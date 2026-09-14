<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-install-msttcore-fonts-on-linux-systems- -->

# How to install msttcore-fonts on Linux systems?

This article applies to all MetaDefender Core V5 releases deployed on Linux systems.

To apply non-English watermarks (e.g., Hebrew, Japanese) in P-DLP or to resolve issues where text becomes corrupted (e.g., characters overlapping) after OCR, additional fonts from Microsoft must be installed on your Linux system.

## [Installation Instructions](/docs/mdcore/knowledge-base/how-to-install-msttcore-fonts-on-linux-systems-#installation-instructions)

1. **Debian/Ubuntu-based Systems**

To install the required font, please issue the following commands.

BashCopysudo apt install fontconfig ttf-mscorefonts-installer
fc-cache -v -r

In case you get an error like `Package ttf-mscorefonts-installer is not available...`, please enable the contrib repository, which contains `ttf-mscorefonts-installer`, by adding **contrib** to the repository lines in **/etc/apt/sources.list** (see below) and then run `sudo apt update`.

BashCopydeb http://deb.debian.org/debian/ bullseye main contrib
deb-src http://deb.debian.org/debian/ bullseye main contrib
deb http://security.debian.org/debian-security bullseye-security main contrib
deb-src http://security.debian.org/debian-security bullseye-security main contrib
deb http://deb.debian.org/debian/ bullseye-updates main contrib
deb-src http://deb.debian.org/debian/ bullseye-updates main contrib

2. **RHEL based systems**

Please first take a look at the package and its content/dependencies to ensure it complies with your regulations.

First, you need to install the dependencies:

BashCopysudo yum install curl cabextract xorg-x11-font-utils fontconfig

Once the dependencies have been installed, you can install the .rpm package itself:

BashCopysudo rpm -i https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm
fc-cache -v -r

3. **RHEL 9 system**

First, install the required dependencies:

BashCopydnf install curl fontconfig cabextract

If you get the following error: `No match for argument: cabextract` you need to enable the EPEL repository:

BashCopysubscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms
dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm

Then, try to install The `cabextract` again:

BashCopydnf install cabextract

The `xorg-x11-font-utils` is also a dependency for the msttcore-fonts-installer, but it is not available in any base RHEL 9 repository, so you need to install the following tools:

BashCopydnf install mkfontscale mkfontdir xset

When you install the msttcore fonts RPM, you need to use the `--nodeps` option so the installation won’t fail because of the missing `xorg-x11-font-utils`:

BashCopysudo rpm -i https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm --nodeps
fc-cache -v -rSupport:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).

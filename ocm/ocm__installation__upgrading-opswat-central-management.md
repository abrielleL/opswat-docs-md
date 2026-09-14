<!-- source: https://www.opswat.com/docs/ocm/installation/upgrading-opswat-central-management -->

# Upgrading OPSWAT Central Management

## [Upgrade OPSWAT Central Management](/docs/ocm/installation/upgrading-opswat-central-management#upgrade-opswat-central-management)

In order to perform an upgrade to a newer version of OPSWAT Central Management , please first uninstall the existing version then follow the steps in [Installing OPSWAT Central Management](/docs/ocm/installation/installing-opswat-central-management) with a new installation package to upgrade the product.

All existing OPSWAT Central Management configuration and data will be kept during the upgrade.

Info

Uninstalling OPSWAT Central Management will not cause any data or settings loss including files, configuration, and license. If you want to perform a clean uninstall and reinstall, please refer to [Clean uninstall of OPSWAT Central Management](/docs/ocm/installation/uninstall-opswat-central-management).

### [Upgrading to version 7.20.0 and newer](/docs/ocm/installation/upgrading-opswat-central-management#upgrading-to-version-7200-and-newer)

From version 7.20.0, OPSWAT Central Management uses Java 11 instead of Java 8. Because of this, when upgrading to version 7.20.0 or newer, you will need to reimport TLS certificates to the new Java 11 distribution. You can find the certificate import instructions at [Adding certificates to Java keystore](/docs/ocm/configuration/adding-certificates-to-java-keystore).

### [(Windows only) Upgrading to version 7.23.0 and newer](/docs/ocm/installation/upgrading-opswat-central-management#windows-only-upgrading-to-version-7230-and-newer)

On Windows system, OPSWAT Central Management version 7.23.0 has a new software requirement: Visual C++ Redistributable Packages for Visual Studio 2013. As of April 2022, the latest version of this software (12.0.40664) is available at <https://aka.ms/highdpimfc2013x64enu>.

You will need to install the aforementioned software before upgrading OPSWAT Central Management to version 7.23.0 or newer.

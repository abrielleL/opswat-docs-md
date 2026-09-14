<!-- source: https://www.opswat.com/docs/ocm/7.39.0/knowledgebase/why-the-ocm-web-management-interface-page-is-not-loading- -->

# Why the OCM Web Management Interface Page is Not Loading?

The OCM Web Management Interface page fails to load, preventing users from accessing the system.

Error message displayed: **For some reason, page couldn’t load**.

## [Cause](/docs/ocm/7.39.0/knowledgebase/why-the-ocm-web-management-interface-page-is-not-loading-#cause)

This issue occurs if the required **Visual C++ Redistributable Packages for Visual Studio 2013** are not installed on the system. The missing dependencies prevent the web interface from functioning correctly.

## [Solution](/docs/ocm/7.39.0/knowledgebase/why-the-ocm-web-management-interface-page-is-not-loading-#solution)

### [**Step 1: Install Visual C++ Redistributable**](/docs/ocm/7.39.0/knowledgebase/why-the-ocm-web-management-interface-page-is-not-loading-#step-1-install-visual-c-redistributable)

1. Download the **Visual C++ Redistributable for Visual Studio 2013** using the link below:

https://aka.ms/highdpimfc2013x64enu

2. Run the installer and follow the on-screen instructions to complete the installation.

### [**Step 2: Restart the OCM Service**](/docs/ocm/7.39.0/knowledgebase/why-the-ocm-web-management-interface-page-is-not-loading-#step-2-restart-the-ocm-service)

1. Open **Services** (services.msc from Run or Start Menu).
2. Locate the **OCM Service** in the list.
3. Right-click and select **Restart**.

### [**Step 3: Verify the Web Interface**](/docs/ocm/7.39.0/knowledgebase/why-the-ocm-web-management-interface-page-is-not-loading-#step-3-verify-the-web-interface)

- Open your web browser and navigate to the OCM Web Management Interface.

## [Conclusion](/docs/ocm/7.39.0/knowledgebase/why-the-ocm-web-management-interface-page-is-not-loading-#conclusion)

Installing the required Visual C++ Redistributable package and restarting the OCM service should resolve the issue.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).

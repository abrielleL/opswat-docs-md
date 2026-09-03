<!-- source: https://www.opswat.com/docs/mdfs/version-6.0.5/installation-guide/issue-trying-to-download-free-trial- -->

# Installation FAQ

**AppExchange is asking me to verify my payment details?**

According to Salesforce there is an issue occurring on their side that might cause an issue when you try to download our app (or some other app). You might encounter a screen such as this one below:

Please follow the instructions on this [link provided by Salesforce](https://trailblazer.salesforce.com/issues_view?id=a1p3A000000EH1aQAG&title=when-installing-an-app-from-appexchange-in-lightning-experience-verify-payment-details-on-the-appexchange-website-displayed-for-free-listing) to solve the issue. If you still have any questions please reach out to [sales-inquiry@opswat.com](mailto:sales-inquiry@opswat.com).

**I am unable to download the app even with the Download AppExchange Packages permission?**

A possible cause for this might be that your Salesforce environment does not allow you to download managed packages (which MetaDefender for Salesforce is). You can view Setup > Package Manager in your Salesforce environment to see if that is the case. If your environment's settings are such that you cannot download a managed package, you will need to contact your Salesforce admin to enable that ability.

**Should I install for admins only or for all users?**

Our recommendation is to install the application for admins only. This way only your Salesforce admins will have access to all the files that are being submitted into the environment and will be the only ones with authority to release files that MetaDefender for Salesforce flags as "infected". If you install for all users, then everyone with access to your Salesforce environment can view the MetaDefender for Salesforce application within Salesforce and all the (potentially sensitive) data that it contains.

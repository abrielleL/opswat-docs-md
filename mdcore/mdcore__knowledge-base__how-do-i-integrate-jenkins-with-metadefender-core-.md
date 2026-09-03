<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-do-i-integrate-jenkins-with-metadefender-core- -->

# How do I integrate Jenkins with MetaDefender Core?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows systems.

#### [Summary:](/docs/mdcore/knowledge-base/how-do-i-integrate-jenkins-with-metadefender-core-#summary)

MetaDefender Core offers a free Jenkins plugin via the MetaDefender Plugin for Jenkins, a free tool from OPSWAT. However, this tool is currently not documented in the MetaDefender Core Knowledge Base (KB).

## [**New Pipeline**](/docs/mdcore/knowledge-base/how-do-i-integrate-jenkins-with-metadefender-core-#new-pipeline)

Create a new pipeline using the 'Freestyle project' option. Use the name 'MD Core' for testing purposes.

## [Test files](/docs/mdcore/knowledge-base/how-do-i-integrate-jenkins-with-metadefender-core-#test-files)

You can scan the test files from the EICAR GitHub repository. Here’s the link for reference: [GitHub - fire1ce/eicar-standard-antivirus-test-files: eicar standard antivirus test files](https://github.com/fire1ce/eicar-standard-antivirus-test-files)

We will then add the steps to build the pipeline with MetaDefender Core

Since this test is performed on a local machine, the API URL is set to <http://localhost:8008/file>

and the API key will be used from the user management API key.

MetaDefender Core

Now, save the configuration and start testing the pipeline by clicking 'Build Now'.

Start the build

Pipe #2

Support:

If you have followed all of the steps above but are still unable to resolve the issue. Please follow these instructions on [How to Create Support Package With Bundle Tools?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-#), before [creating a support case or chatting with our support engineer.](https://my.opswat.com/portal/support)

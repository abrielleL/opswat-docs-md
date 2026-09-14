<!-- source: https://www.opswat.com/docs/mdcloud/account-management/sub-organizations -->

# Sub Organizations

For our professional and enterprise customers that have access to the organization feature, users also have the ability to create sub organizations. You can do this by navigating to your organization on id.opswat.com and clicking the "+ Add Organization" button:

You will then be able to name the new sub organization:

After you name your organization and click the "Add" button, you will be able to allocate API limits to that sub organization you just created by clicking the pencil icon circled in red below (please note, you can only allocate/manage limits to the sub orgs that you create).

Then, you can allocate limits to your sub org by typing them into the boxes and clicking the blue check mark when you are finished.

To invite users to your newly created sub organization, click the blue arrow circled in red below:

As you can see now you are viewing the sub organization you just created. The next step will be to click the users button on the left hand nav:

You will be automatically added as an admin to your sub org and can now add other users to it by clicking the "+ Add User" button:

### [Best Practices for Sub Organizations](/docs/mdcloud/account-management/sub-organizations#best-practices-for-sub-organizations)

1. For our very large customers that purchase one MetaDefender Cloud license for multiple departments and teams within those departments, the sub organization feature allows you have a centrally managed license, yet allocate the appropriate limits to your various teams and let them self manage their MetaDefender Cloud Traffic
2. The sub organizations feature is also a great way to allocate limits to even just a couple API keys. If, for example, your organization is using MetaDefender Cloud in two separate places and you would like to allocate the API limits of each one, simply set up 1 sub org for each of those API keys to allocate limits to it.

### [Example of Sub Organization Use Case](/docs/mdcloud/account-management/sub-organizations#example-of-sub-organization-use-case)

Company 1 has 200 limits total, but chooses to distribute API limits to two (2) Sub-Organizations, 50 to Dept. A and 50 to Dept. B, this would allocate 100 API limits to the Sub-Organizations and leave 100 API limits to the main API Key. Any users assigned to Dept. A would pull from Dept. A limits and any users assigned to Dept. B would pull from Dept. B limits. The users that are part of the parent org and not assigned to Dept. A or B would pull from the remaining 100 API calls per day from the parent organization.

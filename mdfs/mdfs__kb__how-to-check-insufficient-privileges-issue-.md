<!-- source: https://www.opswat.com/docs/mdfs/kb/how-to-check-insufficient-privileges-issue- -->

# How to check Insufficient Privileges issue?

The MDFS application requires two permission sets for each users: "MetaAccess User Access" and "Metedefender User Access", these permission sets are created and assigned to all existing users during the installation process and are assigned to new users when they are created. However, in some cases, the assignments fail dues to several reasons (user license types, ...). When users are missing these permission sets, they will get an "Insufficient Privileges" error when downloading a file.

In this case, the administrator can go to Setup > User > The users have the issues, assign these permission sets to them.

To do the bulk update for all users, please use version 4.2 with the following steps:

1. Check to see how many users are missing the permission sets by: Setup > Developer Console and run this query

SqlCopySELECT Name, Id FROM User WHERE Id NOT IN (SELECT AssigneeId FROM PermissionSetAssignment WHERE PermissionSet.Name = 'Metadefender_User_Access') and IsActive=true

You should see a list of users, please note that some users can't be assigned the permission set dues license type but the regular users should be

2. In Developer Console, open Debug > Open Execute Anonymous Window and run the bellow script

ApexCopyDatabase.executeBatch(new opswat_secrev.AssignPermissionsController(), 20);

The command will execute an update for 20 users in a batch and will take a while to finish, depends on the number of users in the org. By Salesforce design, if one of the users is failed to update, the 20 users won't be assigned the permission. We recommend you to repeat step 1 to check how many users still don't have permission and do step 2 again with smaller user number in the batch until we get expected result.

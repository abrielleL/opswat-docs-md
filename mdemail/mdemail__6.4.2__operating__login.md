<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/operating/login -->

# Login

View as Markdown Ask ChatGPT about this page Ask Claude about this page

To log in to the web management console, users must provide their user name and password according to the user directory they are about to log in to. For details about user directories see [User directories](/docs/mdemail/6.4.2/configuration/users#user-directories).

When the user directory is not specified at the login, Email Gateway Security will attempt to authenticate the user to the default user directory. For details see [Default user directory](/docs/mdemail/6.4.2/configuration/users#default-user-directory).

Login to a non-default user directory

To log in to a non-default user directory, the name of the user directory must prefix the user name, with a backslash `\` character separating the two: `<user directory name>\<username>` .

With the example of the image below, when the user `tramone` wants to log in to the user directory `AD` the username must be provided as `ad\tramone`.

Login to an Active Directory type user directory

To log in to an Active Directory type user directory, it is not the domain that must prefix the username, but the user directory name.

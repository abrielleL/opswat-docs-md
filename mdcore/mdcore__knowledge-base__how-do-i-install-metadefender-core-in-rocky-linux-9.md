<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-do-i-install-metadefender-core-in-rocky-linux-9 -->

# How do I install MetaDefender Core in Rocky Linux 9

When you first install MetaDefender Core on Rocky Linux 9 and successfully complete the installation, some engines may fail to install after activation due to missing dependency packages, as shown below:

The screenshot shows that the Extract Archive Engine failed to install due to missing libraries: **libgdiplus** and **libnsl**. (these dependency packages are requested)

You can install them using the following command:

BashCopycurl https://download.mono-project.com/repo/centos7-stable.repo | tee /etc/yum.repos.d/mono-centos7-stable.repo
yum install -y epel-release
yum install -y libgdiplus --nobest
yum install libnsl -y

**Libnsl** is also a dependency for Deep CDR and other engines. After installing the library, the output should match the screenshot below:

Besides that, the Deep CDR engine requires additional dependency packages (**libgomp**, **ncurses-compat-libs**), which can be installed using the command below:

BashCopyyum install libgomp -y
yum install ncurses-compat-libs -y

The output should be as the image below:

Next, you need to disable and then re-enable the Archive Engine to prompt MetaDefender Core to reinstall it. After doing this, the Archive Engine should install successfully.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

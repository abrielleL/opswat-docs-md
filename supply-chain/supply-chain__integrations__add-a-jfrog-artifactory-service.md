<!-- source: https://www.opswat.com/docs/supply-chain/integrations/add-a-jfrog-artifactory-service -->

# Add A JFrog Artifactory Service

To integrate JFrog with MetaDefender Software Supply Chain, follow these steps:

1. From the left side menu, navigate to **Inventory**, choose **JFrog Binary** or **JFrog Containers** depending on your requirement.

### Connecting JFrog Artifactory

#### JFrog Binary

- This service is used for managing pypis, npm, and other binary repositories.

#### JFrog Containers

- This service is used for managing DockerHub and other container registries.

### Steps to Connect

1. **Give your connection a name** so you can easily identify it later.
2. **Enter your Access Token**. Scroll to the end of this page for more details.
3. **Select Add Connection** to finish the process.

![](https://uploads.developerhub.io/prod/jdK6/qempm9bt11dvcab3db6nvfehhdqawilhuxl2w3fe5tl0bfy4i7g3si7ygwsg4o73.png)

### Where can I find the Access Token?

To generate an Access Token, please follow these steps:

1. **Log in to JFrog Artifactory**.
2. Navigate to **Administration**, than **User Management**, and select **Access Tokens**
3. Click on **Generate Token**. Fill out the form with the necessary details. Then, confirm by clicking **Generate**

> **Info**
>
> By configuring an expiration date for temporary access (e.g., 30 days), the integration with MetaDefender Software Supply Chain will be operational exclusively for the specified duration. Once this period elapses, you will have to create a new token and update the connection.

### Detailed Steps to Add Connection

1. **Name your Connection**: This will help you identify the connection later.
2. **Get your URL**: The URL is the address you use to access your JFrog Container Registry, typically formatted as [**https://your-domain.jfrog.io/**](https://your-domain.jfrog.io/).
3. **Enter your Access Token**:
   - Paste the Access Token generated from JFrog Artifactory.

| **Repository type** | **Support** |
| ---- | ---- |
| Alpine | Yes |
| Ansible | N |
| Bower | Yes |
| Cargo | Yes |
| Chef | Yes |
| CocoaPods | Yes |
| Conan | Yes |
| Conda | Yes |
| CRAN | Yes |
| Debian | Yes |
| Generic | Yes |
| GIT LFS | No |
| Go | Yes |
| Gradle | Yes |
| Hex | No |
| Ivy | No |
| Maven | Yes |
| Npm | Yes |
| NuGet | Yes |
| NVIDIA NIM | No |
| P2 | No |
| PHP Composer | Yes |
| Pub | Yes |
| Puppet | Yes |
| PyPi | Yes |
| RPM | Yes |
| RubyGems | Yes |
| SBT | Yes |
| Swift | Yes |
| Terraform | No |

| **Repository type** | **Support** |
| ---- | ---- |
| Docker | Yes |
| Helm | No |
| HelmOCI | No |
| OCI | No |
| Vagrant | No |

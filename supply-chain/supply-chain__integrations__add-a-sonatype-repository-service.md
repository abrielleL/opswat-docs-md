<!-- source: https://www.opswat.com/docs/supply-chain/integrations/add-a-sonatype-repository-service -->

# Add A Sonatype Nexus Repository Service

To integrate **Sonatype Nexus** **Repository** with MetaDefender Software Supply Chain, follow these steps:

1. Start by creating a Nexus Repository Management service account
2. Go to your MetaDefender Software Supply Chain instance
3. From the left side menu, navigate to Inventory
4. Choose Nexus Binary

> **Warning**
>
> Currently, we only support basic authentication for Nexus Repository. Therefore, we recommend using **HTTPS** for your Nexus instance to ensure secure communication.

### [Steps to Connect](https://www.opswat.com/docs/supply-chain/integrations/add-a-jfrog-artifactory-service#steps-to-connect)

1. Give your **connection a name** so you can easily identify it later.
2. Enter your **Nexus instance URL by providing Nexus instance IP or its Domain**
3. Enter your **Nexus account username**.
4. Enter your **Nexus account password.**
5. **Select** **Add Connection** to finish the process.

![](https://uploads.developerhub.io/prod/jdK6/s48ie8dy5oz0rnrzio5wacdieo0rts3i3jc8b9o60u0okvjsnuhw53pv4t62wuzd.png)

## Supported entities

| Repository Type | Support |
| ---- | ---- |
| APT | Yes |
| CocoaPods | Yes |
| Composer (PHP) | Yes |
| Conan | Yes |
| Conda | Yes |
| Go | Yes |
| HuggingFace | Yes |
| Maven | Yes |
| npm | Yes |
| Nuget | Yes |
| p2 | No |
| Pypi | Yes |
| R | Yes |
| Raw (Generic) | Yes |
| RubyGems | Yes |
| Rust (Cargo) | Yes |
| Swift | Yes |
| Terraform | No |
| Yum | Yes |

| Repository Type | Support |
| ---- | ---- |
| Docker | No |
| Git LFS | No |
| Helm Chart | No |
|  |  |

<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/qualys-cloud-security-agent-not-included-under-patch-management -->

# Why Qualys Cloud Security Agent is not included under Patch Management category when calling DetectProducts

This article is applied to OESIS Framework releases on **Windows** when interacting with **Qualys Cloud Security**.

## [**Overview**](/docs/mdsdk/knowledge-base/qualys-cloud-security-agent-not-included-under-patch-management#overview)

When executing `DetectProducts` with the **Patch Management** category (ID `12`) selected, OESIS Framework may fail to detect **Qualys Cloud Security Agent**.

This behavior occurs because **Qualys Agent** protects its related files using a privileged user. If our SDK runs **without** **elevated permissions**, it cannot inspect the Qualys directory structure to verify if the Patch Management capability is present.

## [**Solution**](/docs/mdsdk/knowledge-base/qualys-cloud-security-agent-not-included-under-patch-management#solution)

Suggestion

**Admin permissions are required** for SDK to detect whether the **Patch Management** module of Qualys Agent is installed on the endpoint.

To resolve this, ensure the SDK is executed with **Administrator/Sudo** privileges. Elevated access is necessary for the SDK to interact with the Qualys Agent and successfully report the agent under the **Patch Management** category for `DetectProducts` method.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

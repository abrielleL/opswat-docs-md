<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-does-omva-agent-not-working-as-expected- -->

# Why does OMVA agent not working as expected?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

If you encounter scenarios where everything is [setup](/docs/mdkiosk/v4.8.6/knowledge-base/how-do-i-set-up-a-media-manifest#utilizing-media-manifest-via-the-opswat-media-validation) correctly on the Kiosk/Core/OCM side regarding OMVA functionality as described below, please consider the following limitation that might be impacting OMVA functionality:

## [Due to faulty settings on the MetaDefender Core side](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-omva-agent-not-working-as-expected-#due-to-faulty-settings-on-the-metadefender-core-side)

- Please make sure the “Skip hash calculation “is not enabled on the MetaDefender Core side on the workflow rule to avoid any OMVA inconsistencies.
- Having this option enabled on the MetaDefender Core workflow-rule will result in the media validation process involving the OMVA agent to not function as expected.

## [Due to faulty time-date settings on the OMVA device](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-omva-agent-not-working-as-expected-#due-to-faulty-time-date-settings-on-the-omva-device)

- Please make sure the date/time is set up correctly on the OMVA machine (on an OS level) to avoid any OMVA inconsistencies.
- Having the wrong date/time setup on the OMVA (in comparison to the MetaDefender Core/Kiosk machine) device might result in the validation process not functioning as intended.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

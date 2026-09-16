<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/is-metadefender-core-able-to-extract--detect-and-block-malicious -->

# Is MetaDefender Core able to extract, detect and block malicious embedded macros?

In short, yes! MetaDefender Core can extract and block files if malicious macros are embedded.

**Macro objects** are typically stored in Office Documents files such as **xlsm, docm, pptm** and so on, kindly make sure that the following option is enabled under your workflow, so that Core can extract Office Documents contents:

Workflow Management > Workflows > [any workflow] > Archive Tab > **Enable extraction of office documents**

Using the MetaScan Engines, it can detect the infected files and directly block them. For a more proactive approach, the DeepCDR Engine ([What is CDR?](/docs/mdcore/v5.22.0/deep-cdr/supported-file-types#what-is-cdr)) is able to deliver a clean version of the file by sanitizing/removing embedded data according to the configuration in place as per each file type, reconstructing the base file.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/language -->

# Language

Summarize Page    Connect to Cursor Connect to VS Code

Under "Settings" → "Language", administrators can configure language (localization).

## [Selecting the Default Language for New Accounts](/docs/mdmft/v3.11.4/configuration/language#selecting-the-default-language-for-new-accounts)

If most users require a non-English language, use this option to change the default language. New users will see texts in the specified language.

## [Adding a Custom Language](/docs/mdmft/v3.11.4/configuration/language#adding-a-custom-language)

By default, MetaDefender Managed File Transfer includes *English*, *Japanese* and *French* languages. Administrators can download these language files and translate the texts to make a new language available in MetaDefender Managed File Transfer.

**Step-by-step Guide to Add a Custom Language**

1. Choose the target language from the list of available languages.
2. Choose the source language from which to translate.
3. Download the source language file.
4. Use a favorite text editor to translate the draft file.

   1. The draft file is a JSON formatted file in the format of “KEY” : “VALUE”, where the value represents the translated text.
   2. This should be an iterative process. It is recommended to translate a few texts, upload the file (step 4) and then check the results.
   3. Some keys may seem cryptic. Contact us by email if assistance is needed in locating these texts.
   4. Best practice is to open a browser and start with commonly seen texts like “OK”, “CANCEL”, “LOGIN”, etc.
5. Upload the translated file.

   1. Validation will take place to ensure that all the necessary key are present, however, you might need to apply some more changes if you find out that some texts do not fit well on the screen.
6. Choose to use this language as the default language for new accounts or change the current language in "User Settings" → "Language" to see the results.

7. Read the information about the upgrade procedure below.

### [Upgrade Procedure with Custom Languages](/docs/mdmft/v3.11.4/configuration/language#upgrade-procedure-with-custom-languages)

Info

The development team consistently adds or removes text with nearly every release due to new functionalities. Repeat the above translation process after each upgrade to ensure all texts are translated.

Follow these steps:

1. After upgrading MetaDefender Managed File Transfer, select the language to update at *step 1***.**
2. Select the same language at *step 2* and download it at *step 3***.**
3. Translate texts still in English (new texts added by the development team).
4. Upload the file after translating the new texts.

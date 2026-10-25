<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-does-icap-server-work-with-password-protected-files- -->

# How Does ICAP Server Work with Password Protected Files?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Password protected files submitted via ICAP are sent to MetaDefender Core for processing.

Core has a Password Storage feature shown here: [Password Storage](https://www.opswat.com/docs/mdcore/operating/inventory-management#password-storage)

If the encrypted file’s password is listed here, Core will process the file just like any other.

If Password Storage does not contain the file’s password it will be marked as failed to scan due to encryption.

Please ensure that you have a full list of commonly used passwords for your organization listed in Password Storage to minimize the latter behavior.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

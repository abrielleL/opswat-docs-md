<!-- source: https://www.opswat.com/docs/mdcloud/knowledge-base/support-for-cors-or-jsonp -->

# Does MetaDefender Cloud support CORS or JSONP?

This article applies to all active MetaDefender Cloud license holders - whether your product is paid for or issued for evaluation purposes.

No, MetaDefender Cloud API does not support CORS or JSONP calls from the client side.

OPSWAT has elected not to enable CORS in current or future releases because it could lead to the practice of including the MetaDefender Cloud API key in client codes, which would expose it to all site visitors.

Please Note:

Support for CORS and JSONP will not be enabled in the future, so the only solution is to defer calling the API through a backend solution.

Support:

For more information on how to **Defer Calling The API Through A Backend Solution**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).

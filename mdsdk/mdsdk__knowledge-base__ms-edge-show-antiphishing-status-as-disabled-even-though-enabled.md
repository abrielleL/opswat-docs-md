<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/ms-edge-show-antiphishing-status-as-disabled-even-though-enabled -->

# Why does Microsoft Edge show anti-phishing status as disabled even though it’s enabled?

### [Problem](/docs/mdsdk/knowledge-base/ms-edge-show-antiphishing-status-as-disabled-even-though-enabled#problem)

The `GetAntiphishing` may return `false` when the SDK runs as a service and no Windows user is logged in. This happens because Edge's Antiphishing feature is enabled or disabled on a per-user basis. Consequently, the SDK returns the Antiphishing status for the current active user session. When no user is logged in, it uses the Local System Account (which is used by programs and services running as Local System), so Edge’s Antiphishing information might not be available in this scenario and `GetAntiphishing` will return `false`.

### [Workaround](/docs/mdsdk/knowledge-base/ms-edge-show-antiphishing-status-as-disabled-even-though-enabled#workaround)

If your main priority is to display Edge’s Antiphishing as `true` under the Local System Account, you can use a workaround by calling the `SetAntiphishing` method and setting the operation to `true`. This only needs to be done once, after which Edge’s Antiphishing will remain enabled under the Local System Account.

<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/why-does-scan-fail-when-clean-is-false-or-omitted -->

# Why does the Scan method fail for some products when clean is false or omitted?

## [Overview](/docs/mdsdk/knowledge-base/why-does-scan-fail-when-clean-is-false-or-omitted#overview)

The `clean` input of the `Scan` method (method id 1006) tells the product whether to try to remediate threats found during the scan.

| Property | Value |
| --- | --- |
| Type | boolean |
| Default | `false` |
| Optional | Yes |
| Platforms | Windows, macOS, Linux |

- `true`: the product scans and attempts to remediate detected threats (clean, quarantine, or delete, depending on the product).
- `false` (default): the product scans and reports threats without remediating them.

Note

Omitting `clean` is the same as passing `clean: false`. The SDK applies the default value before the call reaches the product integration, so leaving the field out does not change the result.

## [What the SDK does when you call Scan](/docs/mdsdk/knowledge-base/why-does-scan-fail-when-clean-is-false-or-omitted#what-the-sdk-does-when-you-call-scan)

1. The SDK fills in `clean: false` if you did not pass it.
2. The SDK hands the call to the integration for the product identified by `signature`.
3. The product integration checks whether the product can run the requested scan with the given `clean` value.
4. If the product cannot run a scan-only operation (`clean: false`), the SDK returns an error and does not start the scan.

This behavior is the same on Windows, macOS, and Linux. Which products are affected depends on the product, and for some products on which scanner component is installed on the endpoint.

## [Error reference](/docs/mdsdk/knowledge-base/why-does-scan-fail-when-clean-is-false-or-omitted#error-reference)

| Return code | Condition |
| --- | --- |
| `WAAPI_ERROR_COMPONENT_METHOD_NOT_SUPPORTED (code -11)` | The product does not support the requested scan with this `clean` value. |
| `WAAPI_ERROR_COMPONENT_METHOD_NOT_IMPLEMENTED (code -12)` | Returned instead of code -11 by some product integrations for the same condition. |
| `WAAPI_ERROR_INVALID_INPUT_ARGS (code -20)` | `clean` was passed with a type other than boolean (returned by some product integrations, and by the SDK when JSON input validation is enabled). |

Codes -11 and -12 can also mean that another requested option is not supported, such as the `scan_type` value. Check the other inputs before assuming `clean` is the cause.

## [Solution](/docs/mdsdk/knowledge-base/why-does-scan-fail-when-clean-is-false-or-omitted#solution)

If `Scan` returns `WAAPI_ERROR_COMPONENT_METHOD_NOT_SUPPORTED (code -11)` or `WAAPI_ERROR_COMPONENT_METHOD_NOT_IMPLEMENTED (code -12)` while `clean` is `false` or omitted, the product only supports scanning together with remediation. Your options:

- If remediation is acceptable for your use case, call `Scan` again with `clean: true`.
- If you need a scan that never changes the endpoint (for example, an audit or compliance check), do not retry with `clean: true`. Treat the product as not supporting a scan-only operation.

Pass `clean` as a JSON boolean (`true`), not as a string (`"true"`) or a number (`1`). Some product integrations reject other types.

Warning

`clean: true` allows the product to remediate every threat it finds. Depending on the product, detected files may be cleaned, quarantined, or deleted. Confirm this is acceptable before enabling it in your integration.

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

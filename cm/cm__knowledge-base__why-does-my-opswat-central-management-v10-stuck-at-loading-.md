<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-does-my-opswat-central-management-v10-stuck-at-loading- -->

# Why does My OPSWAT Central Management v10 stuck at loading?

> **Check Your Version:**
>
> This article applies to all My OPSWAT Central Management version 10.x on-premise

#### Issue

My OPSWAT Central Management v10 management stuck at loading.

#### Possible causes

This loading issue typically occurs due to one the following reasons:

1. CPU architecture incompatibility
   - The server CPU does not support AVX2 instruction set
   - Reference:
     - Intel processors: [How to Know If My Intel® Processor Supports Intel® Advanced Vector...](https://www.intel.com/content/www/us/en/support/articles/000090473/processors/intel-core-processors.html)
     - AMD processors: [Processor Specifications](https://www.amd.com/en/products/specifications/processors.html)
2. Missing dependencies.
   - Required software components are not installed on the server

#### Solution

To resolve this issue, follow these steps in order:

1. Uninstall the current My OPSWAT Central Management v10
2. Verify system requirements
   - Confirm the server CPU supports **AVX2**
   - Install all required dependencies as outlined in the system requirements documentation  [System Requirements - My OPSWAT Central Management](https://www.opswat.com/docs/cm/deployment/system-requirements#software-requirement)
3. Reinstall My OPSWAT Central Management v10

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

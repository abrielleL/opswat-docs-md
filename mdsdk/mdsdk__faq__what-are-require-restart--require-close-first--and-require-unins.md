<!-- source: https://www.opswat.com/docs/mdsdk/faq/what-are-require-restart--require-close-first--and-require-unins -->

# What are require_restart, require_close_first, and require_uninstall_first?

`require_restart`, `require_close_first`, and `require_uninstall_first` are returned when the method runs successfully:

- **require_restart**: A value of 0 means a system reboot is not required after product installation. A value of 1 means a system reboot is required to complete the installation.
- **require_close_first**: A value of 0 means the product and possibly some related products do not need to be closed before installation. A value of 1 means the product and possibly some related products must be closed before installation.
- **require_uninstall_first**: A value of 0 means the product does not need to be uninstalled before installation. A value of 1 means the product must be uninstalled before installation.

**Example**: Suppose a Firefox process is running and `InstallFromFile` executes successfully with a return code of 0 (WAAPI_OK) and `require_close_first` is 1. In this case, it indicates an issue because `require_close_first` with a value of 1 means that Firefox should be closed before running `InstallFromFile` successfully.

<!-- source: https://www.opswat.com/docs/filescan/3.1.1/faq/api-deprecation-and-replacement-notice -->

# API Deprecation and Replacement Notice

**Effective Date: 2026-01-26**

To streamline our API and improve performance, we have removed several deprecated API endpoints. All developers should update their applications to use the new corresponding endpoints as soon as possible.

### [API Endpoint Updates](/docs/filescan/3.1.1/faq/api-deprecation-and-replacement-notice#api-endpoint-updates)

The following table lists the deprecated API endpoints and their replacements.

| Deprecated API Endpoint New API Endpoint | Replacement |
| --- | --- |
| /api/feed/atom | /api/feed/reports |
| /api/feed/info | /api/feed/reports/info |
| /api/feed/archives | /api/archives/samples |
| /api/feed/archives/{publicity}/{type}/{date} | /api/archives/samples/{publicity}/{type}/{date} |
| /api/admin/reports/{report_id} | /api/users/reports/{report_id} |
| /api/users/uploads | /api/reports |
| /api/users/me/uploads | /api/me/reports |

### [Additional Removals](/docs/filescan/3.1.1/faq/api-deprecation-and-replacement-notice#additional-removals)

The backend application and the associated `/api/backend/reputation` endpoint have been removed. This API was unused and had been marked as deprecated.

### [Action Required](/docs/filescan/3.1.1/faq/api-deprecation-and-replacement-notice#action-required)

Please review your code and replace any instances of the deprecated API endpoints with their new counterparts. Continued use of the old endpoints will result in errors.

### [Support](/docs/filescan/3.1.1/faq/api-deprecation-and-replacement-notice#support)

If you have any questions or require assistance with these changes, please contact our support team.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>

<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/what-endpoints-from-mdcore-does-mdss-call -->

# Which API endpoints from MD Core does MDSS utilize?

| Endpoints | Permissions | Usage |
| --- | --- | --- |
| `/file` | Processing result fetching - Self-Only/Anyone  Download processed file - Self-Only/Anyone | Process files and retrieve results Download processed files |
| /readyz |  | System health |
| /stat | System Information - Full | System health |
| /status |  | System health |
| /admin/license | License - Read-Only/Full | License information |
| /version |  | Version information |

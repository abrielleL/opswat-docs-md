<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/why-are-all-endpoints-being-assigned-the-sc-compliant-role- -->

# Why Are All Endpoints being assigned the SC_Compliant_Role?

If the administrator notices that newly connected endpoints are receiving the SC_Compliant_Role instead of the expected roles according to policy, and existing connected endpoints are also being reassigned to SC_Compliant_Role, this may be due to RADIUS enforcement being disabled at that moment.

When RADIUS enforcement is disabled, the system automatically assigns the Compliant role associated with the “All other groups” Policy Group Mapping to all endpoints.

By default, this is “SC_Compliant_ Role”, allowing new endpoints to connect to the network without enforcement. Additionally, a background process updates all non-compliant endpoints, reassigning them to SC_Compliant_Role to ensure network access consistency.

To restore expected role assignments, verify the RADIUS enforcement settings and re-enable enforcement as needed.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

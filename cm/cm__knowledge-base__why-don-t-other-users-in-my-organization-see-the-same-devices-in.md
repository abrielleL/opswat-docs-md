<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-don-t-other-users-in-my-organization-see-the-same-devices-in -->

# Why don't other users in my organization see the same devices in OPSWAT Central Management?

> ** Check Your Version:** This article applies to OPSWAT Central Management (OCM) accessed through the My OPSWAT portal (SaaS/cloud deployments).

## **Issue**

Multiple users in the same [My OPSWAT](https://my.opswat.com/portal/home) organization expect to see the same devices and services when they log in to OPSWAT Central Management (OCM). Instead, each user may see a different (or empty) set of devices, and the roles shown for other users in the User list may not match what those users actually have.

## **Possible Causes**

This occurs because My OPSWAT and OPSWAT Central Management manage users at two different levels:

- **My OPSWAT (Portal)** manages users at the **organization level** — it defines who belongs to your organization.
- **OPSWAT Central Management is multi-tenant.** A single organization can have **multiple service accounts**, and each service account is a **separate tenant (site)** with its own devices and services.
- Each service account maintains its **own list of assigned users and roles**, independent of the organization's user list in the Portal.

Because of this, membership in the organization does not imply access to any particular OPSWAT Central Management service account. A user only sees the devices of the service accounts they have been explicitly invited into — and a user with access to several sites may hold a **different role in each one**. This is also why the roles displayed in the User list can differ from what a user appears to have elsewhere: roles are scoped per service account, not per organization.

**How the levels relate:**

```plaintext
My OPSWAT Organization  (who belongs to the company)
│
├── Service Account / Site A  →  Users + Roles (A)  →  Devices & Services (A)
├── Service Account / Site B  →  Users + Roles (B)  →  Devices & Services (B)
└── Service Account / Site C  →  Users + Roles (C)  →  Devices & Services (C)
A user in the Organization is NOT automatically a user of Site A, B, or C.
The same user can exist in Site A and Site B with different roles.
```

## **Resolution**

### **Invite the user and switch to the shared account**

Follow these steps to grant a user visibility into another user's OPSWAT Central Management account:

1. Log in to My OPSWAT as a user who already has access to the OPSWAT Central Management account (typically the account owner).
2. Go to **User Management > Users** and invite the other users to that OPSWAT Central Management account.
3. Have each invited user log in to My OPSWAT, then go to **Account > Managed Account** and switch to the account they were invited to.
4. Confirm the user can now see the same devices and services as the account owner.

## **Recommendation**

Invite every user who needs visibility into a given OPSWAT Central Management service account directly, rather than relying on shared My OPSWAT organization membership. When a user needs access to more than one site, assign the appropriate role in each service account separately, since roles do not carry over between sites. This keeps device and service visibility consistent for everyone who needs it.

> **Support:** If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

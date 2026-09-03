<!-- source: https://www.opswat.com/docs/my/release-notes/v2026-3-1 -->

# v2026.3.1 - Jul 10th

| **Version** | v2026.3.1.0 |
| ---- | ---- |
| **Release date** | July 10th, 2026 |
| **Release Summary** | This release introduces the **OPSWAT Vulnerability Program**, allowing users to report a security vulnerability in an OPSWAT product and track it to resolution directly in My OPSWAT Portal. It also adds **email as a multi-factor authentication method** for users who cannot use an authenticator app, and gives hardware orders their own dedicated module in the left menu. |

### New Features

#### **OPSWAT Vulnerability Program**

You can now report a security vulnerability affecting eligible OPSWAT products, services, and websites through My OPSWAT Portal, and track it through to resolution, instead of coordinating over email. Reporting is available to all verified My OPSWAT Portal users, subject to geographic eligibility.

This is a part of [OPSWAT Vulnerability Program](https://www.opswat.com/security)

![](https://uploads.developerhub.io/prod/JYvy/khlwq6ljo2mizcwdf8nw8jw779ie7q6vmmffj5bcz79i7x611r9d7izh4s7od8b1.png)

**Further reading: **[Vulnerability Disclosure](https://www.opswat.com/docs/my/others/vulnerability-disclosure)

---

### Enhancements

#### Email-Based Multi-Factor Authentication (MFA)

![](https://uploads.developerhub.io/prod/JYvy/zgwpsmo5i8pncsi17739i65vxp8ratpe6a09yxh47mbmry22ait31x7o513y7tv2.png)

You can now use email as a multi-factor authentication (MFA) method when signing in to My OPSWAT Portal. This gives users who cannot use an authenticator app, for example those working in environments where personal or electronic devices are restricted, a way to complete MFA and reach their account.

During Multi-Factor Authentication (MFA) setup, pick your preferred method on the **Choose an MFA method** screen. You can change your default method anytime in **My Information > Security**

**Further reading: **[Set up Multi-Factor Authentication](https://www.opswat.com/docs/my/my-information/set-up-multi-factor-authentication)

---

#### Hardware Orders Now Move to Left-menu

![](https://uploads.developerhub.io/prod/JYvy/zl79ioyhl0x6nlbcgn4i2u0xah66btn622a1ef2fhfx7g0r5qd3qjnfjkhkbk62u.png)

Hardware orders now have their own **Hardware Orders** section in the left menu, separate from License Management.

Each tab now has an overview panel that summarizes your hardware at a glance: total orders, items that need attention, alongside a status breakdown chart

**Further reading:** [Hardware Orders](https://www.opswat.com/docs/my/hardware-orders/hardware-orders)

---

#### Release Notes Links in the Download Dialog

![](https://uploads.developerhub.io/prod/JYvy/5kra78r8eem7xs5535t067ccye6mn97l8qxv6zs9f34db98m41rqf3b7d3g8q2rz.png)

When you download an OPSWAT product, the download dialog now shows a link to that version's release notes, so you can review what changed before you install. This appears for product versions where the release notes link has been provided.

---

#### End-of-Life Dates for Product Versions

![](https://uploads.developerhub.io/prod/JYvy/gofdzus86qo9p8nsqyvz1c8byzoqnk9b01vxd51yv5t5vjbwxjz22tilbdcci5zo.png)

The download dialog now shows the end-of-life (EoL) date for product versions that follow OPSWAT's support lifecycle policy. You can see how long a version will be supported before you download it.

---

#### Upcoming and On-Demand Webinars

The Webinars section on the Overview page now shows both upcoming and on-demand OPSWAT webinars, so you can register for a live session or watch a past one whenever it suits you.

---

### Bug Fixes

Bug fixes **Registration Activation Email**

Fixed an issue where some newly registered users did not receive their account activation email after signing up.

---

Bug fixes **Custom Identity Provider Sign-In on Microsoft Edge**

Fixed an issue that prevented users from signing in through a custom identity provider (SSO) on Microsoft Edge.

###

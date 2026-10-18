<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/the-mdss-api-gateway---what-it-is-and-which-port-it-uses -->

# The MDSS API Gateway - What It Is and Which Port It Uses

**Applies to:** MetaDefender Storage Security (MDSS) · All supported deployments (Docker on Linux, native services on Windows, Kubernetes)

MetaDefender Storage Security is built from a set of independent services — one that discovers files in storage, one that scans them, one that handles users and permissions, one that manages licensing, and so on. Customers never talk to those services individually. Every request from a browser, a script, or another product arrives at a single service called the **API Gateway**, which checks who is asking, whether they are allowed, and then routes the request to whichever service does the work.

This page explains what that means in practice, which ports a customer needs to open, and how to answer the questions that come up most often in a deployment conversation.

---

## 1. The short version

| Question | Answer |
| ---- | ---- |
| What is the API Gateway? | The single front door into MDSS — for the web console and for all API traffic. |
| Which port does it use? | `8005` (HTTP) and `8006` (HTTPS) internally. |
| Which port does the customer connect to? | `80` (HTTP) or `443` (HTTPS) — the address of the MDSS console. |
| What does the customer open on the firewall? | Just `443` in a standard deployment. |
| Is the API included in the product? | Yes. Every action in the UI is available through the API, at no extra cost or module. |

> **The one thing to remember**
>
> `8005` is the API Gateway's internal port. Customers do not connect to it. They connect to the MDSS console address on **443**, and everything — the UI and the API — is served from there.

---

## 2. What the API Gateway does

Think of the API Gateway as the reception desk of the MDSS deployment. Everyone entering the building goes through it, gets identified, and gets directed to the right department. Nobody walks into a department directly.

It has four jobs:

**It is the only way in.** All other MDSS services run on a private internal network with no exposure to the customer's network. This is the security argument that resonates most: MDSS may be a dozen services, but it presents **one** door to the outside world.

**It authenticates every single request.** Whether the caller is an administrator in a browser, an automated script using an API key, or a user arriving through the customer's SSO provider, the gateway verifies the identity before anything else happens. Nothing reaches a backend service unauthenticated.

**It enforces what each user is allowed to do.** MDSS distinguishes full administrators, tenant administrators, and read-only administrators. The gateway enforces those boundaries centrally, so the rules are applied consistently and cannot be bypassed by calling a service directly. In multi-tenant deployments, it also resolves which tenant a request belongs to and keeps tenants isolated from one another.

**It powers everything customers see and automate.** The web console is driven entirely by the gateway's API, including live scan progress that updates in the browser as files are processed. The same API is what customers use to integrate MDSS into their own tooling.

---

## 3. Ports

### What the customer actually connects to

In every supported deployment, a web front end sits in front of the API Gateway and serves both the console and the API on the same address:

| Port | Purpose | Notes |
| ---- | ---- | ---- |
| **443** | HTTPS — MDSS console and API | The standard, recommended option. Requires a certificate to be configured during setup. |
| **80** | HTTP — MDSS console and API | Enabled by default. Suitable for lab and evaluation environments only. |

A customer browsing to `https://mdss.customer.com` gets the console. A script calling `https://mdss.customer.com/api/...` reaches the API. Same host, same port, same certificate.

### The gateway's own ports

| Port | Purpose |
| ---- | ---- |
| **8005** | API Gateway, HTTP |
| **8006** | API Gateway, HTTPS |

These sit *behind* the web front end. In a Docker deployment they are not published to the host at all — the gateway is reachable only from inside the MDSS internal network. On a Windows native-services installation they are local ports on the MDSS server itself.

Both are configurable at install time if they conflict with something already running on the customer's server. The default of `8005` is what appears in configuration files, support packages, and log output, which is the main reason to know the number.

### What to tell a customer about their firewall

For a standard deployment, one inbound rule:

- **Inbound TCP 80 and 443** to the MDSS server, from wherever administrators and API clients connect.

That is the complete list for reaching MDSS. Ports `8005` and `8006` do **not** need to be opened, and neither do the ports used by the internal services. MDSS still needs *outbound* access to the storage it scans, to the MetaDefender Core scanning engine, and to OPSWAT for licensing — but those are separate conversations, covered in the deployment documentation.

---

---

## 4. FAQ

**"Do we need to open port 8005?"** No. Customers connect on 443. `8005` is internal to the MDSS server.

**"Can we change the port MDSS runs on?"** Yes. Both the front-end port and the gateway port are set at installation and can be changed afterwards. Customers who already run something on 443 commonly move MDSS to another port.

**"Is the API a separate license?"** No. It is included, and it is the same API the MDSS console uses.

**"Can we put MDSS behind our own load balancer or reverse proxy?"** Yes — this is a normal deployment pattern. Terminate TLS at the customer's proxy and forward to MDSS. Bring in Sales Engineering to confirm the specifics for the customer's environment.

**"Does the API support our SSO?"** The gateway handles SSO sign-in for console users. Automated and scripted access uses API keys rather than SSO. Confirm the customer's specific identity provider with Sales Engineering.

**"How is the API secured?"** Every request is authenticated before it reaches any backend service, using either a token, an API key, or an SSO session. Permissions are then checked against the caller's role. Over HTTPS, all of it is encrypted in transit.

---

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

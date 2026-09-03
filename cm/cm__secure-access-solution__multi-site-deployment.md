<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/multi-site-deployment -->

# Multi-site deployment

The Multi-Site Deployment feature for NAC Edges supports hybrid integration between local enforcement components and cloud-hosted My OPSWAT Central Management. NAC Edges communicate directly with local network devices to enforce security policies while receiving configuration and policy updates from My OPSWAT Central Management.

**Key Features:**

- **Independent Operation:** Each NAC Edge functions autonomously, ensuring direct enforcement of security measures at each site.
- **Custom Configuration:** Administrators have the flexibility to configure multiple NAC Edge components, each with unique authentication settings tailored to specific requirements.
- **Multi-Site Capability:** NAC Edges can be deployed across various sites, ensuring consistent security enforcement and policy application throughout the organization.
- **Centralized Monitoring:** The MDITA Cloud portal provides real-time monitoring and visibility into the status and performance of all deployed NAC Edges, enabling effective management and oversight.

Note: Each NAC Edge can only integrate with 1 Virtual Machine. In case you have multiple NAC Edges, then multiple VMs will be required.

## Examples

Create three NAC Edges to represent a deployment across three different sites, with each Edge utilizing a different authentication method.

![](https://uploads.developerhub.io/prod/97qW/xplemi89ykwgu61dkxg9tjqtwhl7ouxyiw8nj629mjvyerzrw9gn16g828c0yep7.png)

- Site A:
  - Client: Unifi-switch

![](https://uploads.developerhub.io/prod/97qW/bp3u6v64e6gj1saz68mh9afj2iuyje5gay4a5iik4fbk0b5ca8kdgug913v5eu1l.png)

- Authentication Method: EAP-TLS (cert-based)

![](https://uploads.developerhub.io/prod/97qW/h6e2qrf39duo5etw65c7j4sfjp0jpstie5ezzumniyif31encogdmxc5krvyt02k.png)

- Site B:
  - Client: Aruba

![](https://uploads.developerhub.io/prod/97qW/m07ysvrgejt3au1purbq70gi4nrllg8ow2tpc2ew5wzd3zf2zexxhnbpz81qyoe0.png)

- Authentication Method: EAP-PEAP

![](https://uploads.developerhub.io/prod/97qW/qxkbnyr4osx6wap1fm4ut4hklrmgi9gpvxtts0o6rii7vbu8joobpyw29plogpaf.png)

- Site C:
  - Client: Cisco

![](https://uploads.developerhub.io/prod/97qW/jn4e9w7hrsw3acdj0ev79xn8n4gnyus0jtotp5rcrtwdpcxj5omlpbrjgq8qeuz2.png)

- Authentication Method: EAP-TTLS

![](https://uploads.developerhub.io/prod/97qW/x2bmxgrdkvo8hlqw0h96cl7l4yupwm1i6d1cw2b1sun20j1c0bw270njjdtwnfvi.png)

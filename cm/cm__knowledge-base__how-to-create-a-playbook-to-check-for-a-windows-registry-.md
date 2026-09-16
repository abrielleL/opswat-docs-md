<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-to-create-a-playbook-to-check-for-a-windows-registry- -->

# How to create a playbook to check for a Windows Registry?

> **Check Your Version:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows My OPSWAT Central Management IT Access

Playbook checks whether a Windows Registry Key and Value Exists

If TRUE, mark the device as Compliant

If FALSE, mark the device as Non-Compliant

## Outline

![](https://uploads.developerhub.io/prod/97qW/55n3yx1rc4anlyg61rwh3wtxhnd7552z18zzzhrprh4e48fs5fv5kyuk6i4m782n.png)

## Registry

We are checking if the “global” key exists, with the value/string “restport”

![](https://uploads.developerhub.io/prod/97qW/er1puvqng6qdm4nq2rmqxao2vmkaajkuh4mrzy8fllvouv0mwmvwwexvnq8lr0we.png)

## Task

Registry key: HKEY_LOCAL_ MACHINE\SOFTWARE\OPSWAT\Metascan\global

> **Warning:**
>
> We are removing the Computer\ from the path

![](https://uploads.developerhub.io/prod/97qW/uzt1n0qkfur86050yiay5ctr8pnzpp5dzcmijfs9z3ra3e8o6mqtt90kud0zpb00.png)

## Conditional Node

![](https://uploads.developerhub.io/prod/97qW/59vkgxtxqbo3u6z0bv0trg6jrh38225ws89giob162wp8zvh4kf93683kro949i4.png)

## Actions

Left: Returns compliant if the registry exists

![](https://uploads.developerhub.io/prod/97qW/4e94byn8qerezej9lc42ov13k2gu8cjcjlcorb7wkpj4y9qy0x87juwpwjnnn6z9.png)

Right: Returns non-compliant if the registry does not exist

![](https://uploads.developerhub.io/prod/97qW/de2o1cmp5dc0k7m0pmq6o4ma60auk18ylr9sejrrg83me7ie4f114cxfrdtzdt5w.png)

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

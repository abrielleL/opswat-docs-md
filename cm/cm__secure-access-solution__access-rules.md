<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/access-rules -->

# Access Rules

> **Info**
>
> This only applies to IdP MFA, SAML Single Sign On Based and Next Generation Methods

My OPSWAT Central Management supports you configure conditions to block/allow a device from accessing specific applications or any applications based on device posture status and groups. You can configure multiple access rules like you do with access control list on Firewall. My OPSWAT Central Management processes access rules in order to make decision on granting an access.

## Managing access rules

1. Log into the My OPSWAT Central Management console
2. Navigate to **Secure Access** and then **Rules**
3. To re-order rules:

- drag and drop a rule
- click the arrow icon to move rules up and down

4. To delete a rule: click the trash icon on the rule
5. To view details of a rule: click on the rule or the expand icon at the end

![](https://uploads.developerhub.io/prod/97qW/hsj09101fx3s2999tj51t40dqe5vzu71n690ud5dzsg6zbjhklj0augkf1w4kae3.png)

6. Click APPLY and enter your PIN to confirm changes. All changes will not be applied until you complete this step.

## Add a new access rule

1. Log into the My OPSWAT Central Management console
2. Navigate to **Secure Access** and then **Rules**
3. Click "**ADD NEW RULE**"
4. With a new access rule, you need to specify how you would like to block/allow a device from accessing your applications

![](https://uploads.developerhub.io/prod/97qW/3z4xk1s6nrgkofalzikd0lj8n2erqr1mkaf3tz166e7ic8jf3calrz72asq73a2l.jpg)

- *Rule name*: a rule name, for example *Block non-compliant devices*
- *Action*: Block or Allow a device from accessing applications.
- Applications will be applied: select available options in the selection dropdown
- *Any*: to apply the rule to all applications
- *Specific*: to apply the rule to specific applications. You need to specify what applications you would like to apply this rule by selecting applications in the "Select Applications" list.

![](https://uploads.developerhub.io/prod/97qW/q77sqba9dhv9mj721d19c1v2ksoppb71q8sfq2ac8lgy4raztdhqh3uvut6u8f2a.png)

*Notes:*

*If you add a new application, you need to update this rule if you would like to apply to the application.*

*If you delete applications, they will be removed from the list automatically. In case, there is no applications in the list, the rule is considered as in-valid and never been processed. This situation can be happened when you delete all applications you configured.*

- Rule Conditions: all conditions need to be met to pass the rule.
- Agent status:
- Agent is not installed: this condition is met if a device has not installed MetaDefender Endpoint.
- Agent is installed: this condition is met if you require MetaDefender Endpoint is installed and the device status
- Device status: if this condition is checked. My OPSWAT Central Management checks device status for this rule.
- Device is in groups: if this condition is checked, My OPSWAT Central Management will check if a device is in groups specified in the rule. Otherwise, My OPSWAT Central Management doesn't consider what group a device is assigned to.
- any: no matter what group a device is assigned to, this condition is always met.
- specific: this condition is met if the device is in the specified groups. You need to select groups you would like to apply to the rule.

![](https://uploads.developerhub.io/prod/97qW/yx3udi5dga67ug3xqbbvxiluqfvp24l67qhr9kkrd1eqjuz1kovtemt673hz5vxt.png)

*Notes:*

*- if you add a new group to your account, you need to update this rule if you would like to apply to the group.*

*- if you delete a group which configured in the rule, the group will be auto-removed from the specified groups.*

5. Click **ADD RULE**
6. Click **APPLY** and enter your PIN to confirm the change

## Example rules

1. Allow mobile devices to access all applications

![](https://uploads.developerhub.io/prod/97qW/d0pwwm7eeb4jkkfblt0yfta3yet6gpwfvbzyqzm3gc52898ttvwa1q7d5jko3xq5.png)

2. Block all unknown devices, that have not installed MetaDefender Endpoint, from accessing any applications

![](https://uploads.developerhub.io/prod/97qW/li1ud0kg6jdd2j74swy2zpsc069hgfis0nsjn3w7dbyigervns7aeq38pvrod3ec.png)

3. Block all non-compliant devices from accessing any applications

![](https://uploads.developerhub.io/prod/97qW/mu28cmae7q8cs4o3arx8wzcui84jdl16gp2y7wzgdyfn47dkpsa7w3e66a7we30o.png)

4. Allow only compliant/exempted devices in group Accounting to access Salesforce application

![](https://uploads.developerhub.io/prod/97qW/zaosrostk79o4t1fd0ej3itv4funopbw81bx1hp3iqbbvzwgxiyguxdexrjnxqam.png)

5. Block all devices in the group block-list to access to all applications

![](https://uploads.developerhub.io/prod/97qW/tv5qlqn3fx8l7aj6eadzx1hvo64ejcfvtnpv9h70s9lpok7zlybq2upb4fty7ny2.png)

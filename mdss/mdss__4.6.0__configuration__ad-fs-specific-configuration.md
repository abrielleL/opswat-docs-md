<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/ad-fs-specific-configuration -->

# AD FS Specific Configuration

> **Info**
>
> To properly access MDSS, the following AD **Security Groups** are required:
>
> - **SsoAdministrator** - the equivalent of local MetaDefender Storage Security administrator role
> - **SsoReadOnlyAdministrator** - the equivalent of local MetaDefender Storage Security read-only role
>
> It is also necessary for the AD user to have an **email address** set up, so that it is set as the MetaDefender Storage Security's user email

To set up AD FS SSO for MDSS, follow these steps:

1. Within the AD FS settings, navigate to the "**Scope Descriptions**" directory and click "**Add Scope Description**"

![](https://uploads.developerhub.io/prod/k8zL/stsxkqmo916wl1g7pnqd350iifvnmxirf5xmggoo38yq1b1kyi2chkfbiizvdhqz.png)

2. Create a scope with the name "**offline_access**"

![](https://uploads.developerhub.io/prod/k8zL/qvo7e944r2chx2a21wjmrlcf9nxd4rim6uyaz8hhdug65xz6i5i34s1hzqrdfhmw.png)

3. Navigate to the "**Application groups**" directory and click "**Add Application Group**"

![](https://uploads.developerhub.io/prod/k8zL/keuvng5xqx81erhn3j0vg4vobdgcn3n9hgxb2wu7g65s1amt8012c32bydke9csu.png)

4. Give your application any name you like and for the template, select "**Server application accessing a web API**"

![](https://uploads.developerhub.io/prod/k8zL/mo5dzdykz7hgbtaocralo5abms5ae5cpqur5qwltjwzgxed7bz4r61mjwow5d301.png)

5. Give the server app a name, save the generated **Client Identifier** somewhere, and as the "**Redirect URI**", write the the base URL of the MDSS deployment, followed by the "**/callback**" suffix.

![](https://uploads.developerhub.io/prod/k8zL/xhe90sdsnfae45ip72is3ebnntau6sj9e8tm0enjpljhlhlqy0pr98ppjnry80za.png)

6. Select "**Generate a shared secret**" and store the secret somewhere

![](https://uploads.developerhub.io/prod/k8zL/cx3vlm9bfjoyt3ppzd6rmuobvygyro476er73v0sgnydsv499f8d8b2xiqhyvpon.png)

7. For the "**Identifier**" field, put the previously generated **Client Identifier** that you saved

![](https://uploads.developerhub.io/prod/k8zL/0eji72kaj2hmvgcx94aymoambyowxdvxpyvgr5x7rv8hv7ov2cfmae6567222msx.png)

8. For the access **control policy**, select "**Permit everyone**"

![](https://uploads.developerhub.io/prod/k8zL/gc4fz5xwzdapqy1knaxxaqz3korazh0kfmtvbj5uttfi3jy2wwvk92nit5mafrel.png)

9. For the **permitted scopes**, select the following from the list: **allatclaims**, **email**, **offline_access**, **openid**, **profile**

![](https://uploads.developerhub.io/prod/k8zL/67c2h4p4udg5tfjf8068pc8okoxclj295okqqbwvc58g9kn80d0hvajlcuvg0x6x.png)

10. After saving the created application group, select it and click on **Properties**

![](https://uploads.developerhub.io/prod/k8zL/0z0y4ppdashyevkh6fzt1x32spm210psu8qoaa0j52npqm6r7xvcim0l116z5u05.png)

11. Select the configured **Web API** and click on **Edit**

![](https://uploads.developerhub.io/prod/k8zL/dwlev91owvcvjqek5i98ly1lbx2lm0ooy33dtuqp7nekm6m8capqm2ht4hzt5psu.png)

12. Go to "**Issuance Transform Rules**" and click "**Add Rule**"

![](https://uploads.developerhub.io/prod/k8zL/bwlgzw6zluvijrywqg5qluxcpfbuvizmqjz98ujzefn5rrhhmgs6i1gbck0qs8ar.png)

13. Select "**Send LDAP Attributes as Claims**" as the **Claim Rule Template**

![](https://uploads.developerhub.io/prod/k8zL/w7od3faa9pn4jgg6qevps26u0k4zmtzihx3hhzfhmew98hcpvn858pzfrxd8y5v3.png)

14. Give the rule a name, select Active Directory as the attribute store and configure the following:

- **E-Mail Address** as **E-mail Address**
- **Is-Member-Of-DL** as **" groups*****"***
- **Display-Name** as ***"user_display_name"***

![](https://uploads.developerhub.io/prod/k8zL/fvy4i0dinynp2fyayo9luzn8rzcnngmk0cvup4cl6pogzw80mw7adi8h5v4nlxmu.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

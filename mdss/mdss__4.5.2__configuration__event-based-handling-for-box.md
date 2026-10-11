<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/event-based-handling-for-box -->

# Event-based handling for Box

MetaDefender Storage Security has a generic webhook endpoint that can be invoked through the Box Webhooks. These monitor Box content for events and notify you whenever an event occurs.  There are two types of Box Webhooks: V1 and V2, but only V2 is supported by MetaDefender Storage Security

## How to create Box Webhooks

1. Log in to [Box](https://www.box.com/) and then go to [Developer Console](https://app.box.com/developers/console)
2. If you do not have an existing app, create a new one (Please check [How can I generate a public/private key pair](https://docs.opswat.com/mdss/integrations/add-a-box-storage#how-can-i-generate-a-public--private-key-pair))

> **WARNING**
>
> Box V2 Webhooks can only be created when the scope Manage Webhooks is selected and the application has been authorized

3. Navigate to your application
4. Select the **Webhooks** tab
5. Click the **Create webhook** button

![](https://uploads.developerhub.io/prod/k8zL/vp8etk0p07pjnjmk01r7pjinbvxjqa86vu9rx38x1qc20v22nlbfs1i9y7mhthuy.png)

6. Select **V2** from the drop-down list

![](https://uploads.developerhub.io/prod/k8zL/0bk1811a3zpl5ubwlq802e5x4ecuubkx6rs5drafofablwri4gurfixbfjezmkfy.png)

7. Fill in the form:
   1. Enter the **URL address** that will be notified when the webhook is triggered (the address where MetaDefender Storage Security is hosted)

> **WARNING**
>
> URL Address must have a secure URL (HTTPS)

![](https://uploads.developerhub.io/prod/k8zL/qp6wy72oeje8r0xnei2zjnvujksb4aslyoww0b78wyhznq5tly38gq0qrn49e85y.png)

b. Select the folder that you have set in MetaDefender Storage Security as the element that triggers the webhook

c. Choose **File Uploaded** as the trigger for the selected folder

![](https://uploads.developerhub.io/prod/k8zL/yo8o84v6uq6ploe81asr12uqulnqafitxghin7j2gwpci0q786zmcefth9dqlbuf.png)

8. Click the Create webhook button to save your changes
9. **Copy the ID** of the generated webhook to enter into MDSS

![](https://uploads.developerhub.io/prod/k8zL/bcyx9lcpzmx0t4hud15xt72u2g0j1pngm4abv0xaa73pho5flz0s6fmrebtwcnff.png)

10. Enter the copied webhook ID into the edit storage form for your Box storage

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)

<!-- source: https://www.opswat.com/docs/mdss/4.4.2/configuration/event-based-handling-for-box -->

# Event-based handling for Box

MetaDefender Storage Security has a generic webhook endpoint that can be invoked through the Box Webhooks. These monitor Box content for events and notify you whenever an event occurs. There are two types of Box Webhooks: V1 and V2, but only V2 is supported by MetaDefender Storage Security

## [How to create Box Webhooks](/docs/mdss/4.4.2/configuration/event-based-handling-for-box#how-to-create-box-webhooks)

1. Log in to [Box](https://www.box.com/) and then go to [Developer Console](https://app.box.com/developers/console)
2. If you do not have an existing app, create a new one (Please check [How can I generate a public/private key pair](https://docs.opswat.com/mdss/integrations/add-a-box-storage#how-can-i-generate-a-public--private-key-pair))

WARNING

Box V2 Webhooks can only be created when the scope Manage Webhooks is selected and the application has been authorized

3. Navigate to your application
4. Select the **Webhooks** tab
5. Click the **Create webhook** button

6. Select **V2** from the drop-down list

7. Fill in the form:

   1. Enter the **URL address** that will be notified when the webhook is triggered (the address where MetaDefender Storage Security is hosted)

WARNING

URL Address must have a secure URL (HTTPS)

b. Select the folder that you have set in MetaDefender Storage Security as the element that triggers the webhook

c. Choose **File Uploaded** as the trigger for the selected folder

8. Click the Create webhook button to save your changes
9. **Copy the ID** of the generated webhook to enter into MDSS

10. Enter the copied webhook ID into the edit storage form for your Box storage

<!-- source: https://www.opswat.com/docs/my/troubleshooting/support-chatbot-not-working -->

# Why doesn’t the Support Chatbot function as expected?

If an issue occurs when using the chatbot and it fails to load properly, the screen below may appear at the start of the chat.

This typically happens because the customer's network environment blocks specific URLs required for the chatbot to function. For example, a firewall or proxy might restrict outbound access to the chatbot’s hosting service.

When this happens, the chatbot will not function as expected and will appear as shown below:

![](https://uploads.developerhub.io/prod/JYvy/nzu94uwnmpiuh1yj04g7km2l70lhqytcob2buzngrcf16n5tt6gv3f1e567f229v.png)

## How to fix it

To resolve this issue, allow the following URL on your firewall or network security system: [**https://webchat.botpress.cloud**](https://webchat.botpress.cloud)

Once access to this URL is granted, the chatbot  should load normally and be fully functional.

![](https://uploads.developerhub.io/prod/JYvy/xynsajig8ljr8by94m5hnsqqduu3hcm45b4u60qd3d0wbb4ckctilr4qappdtgal.png)

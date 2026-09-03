<!-- source: https://www.opswat.com/docs/mdendpoint/validation-endpoint/administrator-console -->

# Administrator console

The **Challenge and Response** feature can be accessed on the MyOPSWAT portal, which you can find at the following URL: https://my.opswat.com/product-management/settings/tools. Alternatively, this feature is also available for use in the MyOPSWAT OnPrem environment.

**Step 1:** **Input the challenge code bring by client**

Administrators access Central Management > Settings > Tools to input the challenge code that client bring:

![](https://uploads.developerhub.io/prod/2x2P/jopbiwezzdcu8qzefy0aspe3zisf5nh1pe99g76d0cwc5kx5mfr5x26lrsx4uiu4.png)

**Step 2:** **View detail of request that generate this challenge code**

View detailed information on requests, including device identity and command name. Administrators can review client requests to approve, generate a response string, or reject them.

![](https://uploads.developerhub.io/prod/2x2P/yhpa4467tmpbifk0xzner3777bklwg21h1q8uyy9sjnx0tyjk32qebsidmfoffnv.png)

**Step 3: Input the required fields to generate the response**

Administrators have to input some fields that are needed for the response generation process:

- Command parameters
- The user request (to be logged by My OPSWAT)
- Expiration time of this response
- Password: important to note that this is not the password of My OPSWAT account, this password is the installation password that is used when the administrator installs MDE. If the admin does not set the password, MDE will use the default (“Opswat1234!“)

![](https://uploads.developerhub.io/prod/2x2P/6yrg29cv7avcs9z7iazjlkl2xsqzmv3l1s176ofpz9bl9j04a71kl9vemlg7psb9.png)

**Step 4: Provide the client with the response code to approve this request**

The user will receive this response code to run the requesting command.

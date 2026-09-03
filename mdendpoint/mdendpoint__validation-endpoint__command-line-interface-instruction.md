<!-- source: https://www.opswat.com/docs/mdendpoint/validation-endpoint/command-line-interface-instruction -->

# Command-line Interface Instruction

**MetaDefender Endpoint Standalone** provides a faster and native solution to generate challenges and input responses for executing commands that require admin approval. This applies to actions performed via the command-line interface (CLI).

The CLI supports the commands listed in the Introduction section above, using the process “**mde-service.exe**“ located in the installation folder to perform the actions. This help command also explains how to generate a challenge and input the response, also referred to as an OTP (One-Time Password)

![](https://uploads.developerhub.io/prod/2x2P/h0hdqlxrwc0qy6xjds77jbxhpnek1pf1ec16fjaedaxkeyfa7l5q8gvgdzt8od6g.png)

(1) Execute the help command.

(2): Introduction on using challenge and response in help command.

---

**In this scenario, we add devices with the vendor name "Kingston" to the allow list. Here are the detailed steps to using this feature via CLI:**

**Step 1:** Generate challenge string with the command need to be executed

Execute command without adding --password or --otp flag to generate the challenge code:

![](https://uploads.developerhub.io/prod/2x2P/ztlljns5pghmcq4b6qufejt5m5y6lrwmxyf0jurb9avetd7al1gido0u2up94y4p.png)

**Step 2:** Bring the challenge code to the administrator and get the response

The admin will determine whether the client can execute the command. If approved, the admin will provide the client with the response code needed to execute the requested command. The process by which the admin views and approves these requests is detailed in the section for the administrator console.

**Step 3:** Execute the command in the first step with response from admin

After receive approval from admin and get response, execute the command in step 1 and add --otp flag" should be "After receiving approval from the administrator and obtaining the response, execute the command from step 1, adding the --otp flag:

![](https://uploads.developerhub.io/prod/2x2P/ledhzjl3s8heg6i9kti0j7igsn7u0ro8ry85cvkzu2jh83cxvauo24in7p4vuu5s.png)

<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t -->

# How to Simulate a Test Email to Verify EGS Functionality Using Telnet?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Telnet Installation](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#telnet-installation)

### [**Windows:**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#windows)

Make sure Telnet is enabled under "Turn Windows features on or off."

### [**Linux:**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#linux)

Make sure Telnet is installed on your system.

#### [**Debian/Ubuntu-based distributions:**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#debianubuntu-based-distributions)

BashCopysudo apt install telnet -y
#### [**RHEL/CentOS/Fedora:**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#rhelcentosfedora)

BashCopysudo yum install telnet -y
#### [For newer versions (CentOS 8+, RHEL 8+, Fedora):](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#for-newer-versions-centos-8-rhel-8-fedora)

BashCopysudo dnf install telnet -y
#### [Verify Installation:](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#verify-installation)

After installation, check if Telnet is installed by running:

BashCopytelnet --version
## [Turn off this option to allow EGS to accept the test email.](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#turn-off-this-option-to-allow-egs-to-accept-the-test-email)

## [Simulate Email using Telnet](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#simulate-email-using-telnet)

### [**1. Connect to the SMTP Server**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#1-connect-to-the-smtp-server)

Open a terminal and use Telnet to connect to the SMTP server on port **10025**

BashCopytelnet smtp.example.com 10025

Replace `smtp.example.com` with the actual SMTP server address.

### [**2. Greet the Server (HELO/EHLO)**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#2-greet-the-server-heloehlo)

Once connected, introduce yourself:

BashCopyHELO test.com

If the server supports **EHLO**, it will respond with additional SMTP options.

### [**3. Specify the Sender's Email**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#3-specify-the-senders-email)

Use the `MAIL FROM` command to specify the sender:

BashCopyMAIL FROM:<user@test.com>

The server should respond with `250 OK` if accepted.

### [**4. Specify the Recipient's Email**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#4-specify-the-recipients-email)

Use the `RCPT TO` command to define the recipient:

BashCopyRCPT TO:<user2@test.com>

Again, you should receive a `250 OK` response.

### [**5. Composing the Email**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#5-composing-the-email)

Use the `DATA` command to start the message:

BashCopyDATA

You should see a prompt like `354 End data with <CRLF>.<CRLF>`, indicating that you can now enter the email content.

### [**6. Enter Email Content**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#6-enter-email-content)

Type the email body using the following format. A line must be added between the header and the body of the email.

BashCopySubject: Test Email from Telnet
From:user@test.com
To:user2@test.com
This is a test email sent using Telnet.
.

**End the message with a single period (**`.`**) on a new line**, then press **Enter**.

### [**7. Confirm and Send**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#7-confirm-and-send)

The server should respond with something like:

BashCopy250 OK: queued as XYZ123

This confirms that the email has been accepted for delivery.

### [**8. Close the Connection**](/docs/mdemail/6.4.2/knowledge-base/how-to-simulate-a-test-email-to-verify-egs-functionality-using-t#8-close-the-connection)

To exit, type:

BashCopyQUIT

You should see a `221 Bye` response.

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).

<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-to-encode-data-in-base64- -->

# How to encode data in Base64?

Summarize Page    Connect to Cursor Connect to VS Code

Various applications and scenarios tend to make use of the Base64 Encoding when sending data. In such cases, users may wish to test different functionalities manually, by sending different calls to the system.

For instance, MetaDefender Managed File Transfer will require Login Credentials encoded in Base64 for performing the Authentication API:

The presence of escape characters ( \r \n ) might complicate things a little, so in this case we want to make sure that our encoding is correct. One way of successfully and correctly encoding this would be making use of the Java Programming Language, and running a script like the one below:

JavaCopyimport java.util.Base64;
public class Main {
public static void main(String[] args) {
String originalString = "JohnDoe\r\nSecretPassword ";
// Encode the string to Base64
String encodedString = Base64.getEncoder().encodeToString(originalString.getBytes());
// Print the encoded result
System.out.println("Encoded String: " + encodedString);
}
}

That would provide us with the Encoded String: Sm9obkRvZQ0KU2VjcmV0UGFzc3dvcmQ=

Alternatively, you can also use PowerShell:

PowershellCopy# Define the original string
$originalString = "JohnDoe`r`nSecretPassword "
# Convert the string to bytes using UTF-8 encoding
$bytes = [System.Text.Encoding]::UTF8.GetBytes($originalString)
# Encode the byte array to Base64
$encodedString = [Convert]::ToBase64String($bytes)
# Print the encoded result
Write-Output "Encoded String: $encodedString"

Which we can further use to our scenario, as needed.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

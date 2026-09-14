<!-- source: https://www.opswat.com/docs/mdcloud/account-management/rsa-key-encryption -->

# RSA Key Encryption

## [What Is an RSA Key and How Does It Work?](/docs/mdcloud/account-management/rsa-key-encryption#what-is-an-rsa-key-and-how-does-it-work)

RSA is a public-key cryptosystem that is widely used for secure data transmission. It was developed by 3 MIT faculty members in 1977. An RSA key (or rather pair of keys) is an asymmetric encryption method that allows users to securely send data to one another. Here's how it works...

- Bob needs to send a file to Alice but Bob is very security conscious and wants to encrypt the file to make sure no one else can get a hold of it. Thus, Bob tells Alice that he wants to use RSA keys to securely send her the file.
- Bob and Alice both generate RSA keys using the RSA algorithm. When they do this, each of them receive *a pair of keys*: one public and one private.

  - The keys are mathematically linked but even if you get a hold of one, you cannot generate the other
- Bob will encrypt his message using *Alice's public key*. Her public key can be shared with anyone she wants to share data with.
- After Bob sends his message encrypted with Alice's public key to Alice, she can then decrypt the message *with her private key* (which is the only way to decrypt a message sent with her public key)

A good analogy of RSA key encryption is your address and your mailbox. You can give out your address to anyone that wants to send you mail (like your public key). However, only you have the key to your mailbox (your private key) and so you are the only one that can open your mailbox (or decrypt) and read the messages sent to you.

## [Why Use an RSA Key for MetaDefender Cloud?](/docs/mdcloud/account-management/rsa-key-encryption#why-use-an-rsa-key-for-metadefender-cloud)

1. RSA keys enable you to make secure webhook calls. API clients are able to verify the authenticity of a webhook request using the private RSA key if configured, allowing for increased security.
2. RSA keys allow for end to end encryption. The file(s) will be encrypted in a way such that only the user with the private key can decrypt the file when the encryption is enabled for the account.

## [How to Generate an RSA Key](/docs/mdcloud/account-management/rsa-key-encryption#how-to-generate-an-rsa-key)

You can generate an RSA key online (simply googling RSA key generator will provide you with a lot of options). You can even do it from the command line interface of your computer.

## [How to Set Your RSA Key](/docs/mdcloud/account-management/rsa-key-encryption#how-to-set-your-rsa-key)

Log in to your OPSWAT account and navigate to the "Security" section on the left hand menu. From there you will be able to set your RSA key by clicking the button "Set RSA Key". Please note that we are asking for ***your public key*** (not your private key). After you have set up your RSA key, you will be able to view the key in the same place and change it if you need to later on.

## [How to Perform Secure Webhook Calls With An RSA Key](/docs/mdcloud/account-management/rsa-key-encryption#how-to-perform-secure-webhook-calls-with-an-rsa-key)

Here is the process to use an RSA key to make secure webhook calls with MetaDefender Cloud

1. MetaDefender Cloud - side

   1. MetaDefender Cloud will include an additional `signature` field in each webhook call with the current timestamp value encrypted using the RSA public key provided to them (please see [How to Set Your RSA Key](/docs/mdcloud/account-management/rsa-key-encryption#how-to-set-your-rsa-key)).
2. Client-side

   1. The client can verify the timestamp value by decrypting the `signature` field using their RSA private key. As only the client will have the private key, only they can decrypt the `signature` field.

## [How to Encrypt Sanitized Files With An RSA Key](/docs/mdcloud/account-management/rsa-key-encryption#how-to-encrypt-sanitized-files-with-an-rsa-key)

Here is the process to use an RSA key to encrypt sanitized files with MetaDefender Cloud:

1. MetaDefenderCloud-side

   1. When a file is sent to to be sanitized, generate a symmetric key → SKey
   2. Then, encrypt the symmetric key using the RSA public key → ESKey

      1. *We need to use a symmetric key because RSA keys can only encrypt files up to 256 bytes, which is often less than the size of sanitized files*
   3. Third, send the ESKey back to the client in the scan response
   4. Next, when the sanitization is complete, use the SKey to encrypt the sanitized file and store it in S3
   5. Lastly, discard (delete) the SKey

      1. *This final step ensures that not even OPSWAT can access that sanitized file*
2. Client-side

   1. The client sends a file to be sanitized
   2. Then the client decrypts the ESKey received in the response using their private RSA key to obtain the SKey
   3. The client can then download the sanitized file and decrypt it using the SKey
   4. The client can then discard the SKey

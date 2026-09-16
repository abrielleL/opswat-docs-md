<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/cloud-deployment/customize-ami -->

# Customize OPSWAT MetaDefender AMI from Marketplace

Please follow these instructions before generating a custom AMI from the OPSWAT AMI published in the AWS marketplace.

- Default username and password is `admin`/`<instance-ID>`

  - “admin” is an unacceptable password. Whenever the end-user changes the password to “admin”, it will automatically change the password to `<instance-ID>` after the Instance is rebooted.
- To create custom AMI from OPSWAT AMI, some mandatory things need to be noted before converting:

  1. ***(*** ***Required*** ***)*** Deactivate the MetaDefender Core license in the EC2 instance from where the new AMI will be created.
  2. ***(*** ***Required*** ***)*** Not to add any parameters during the creation process.
  3. ***(*** ***Optional*** ***)*** Change MD Core password.

     - If the end-user changes the password to “admin”, their default password after creating a custom AMI will be `<instance-ID>`
     - If the end-user does NOT change the Core UI password, it will be the default password in the original instance (instance-id) for all the new instances that uses the custom AMI.

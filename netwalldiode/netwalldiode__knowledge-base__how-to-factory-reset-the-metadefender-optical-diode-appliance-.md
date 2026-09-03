<!-- source: https://www.opswat.com/docs/netwalldiode/knowledge-base/how-to-factory-reset-the-metadefender-optical-diode-appliance- -->

# How to factory reset the MetaDefender Optical Diode appliance?

This article applies to Versions of MeteDefender Optical Diode 1.6.0 and above.

Requirements:

To perform the following actions, you will need access to the CLI. This can be done either by connecting a keyboard and a monitor to the product or, if you have SSH enabled, you can open an SSH connection.

Please note that you will need to provide credentials to be allowed in.

There are two options to cleaning all data from the product, one more destructive than the other:

## **Method One (Flush configuration)**

You can flush all the configuration settings, network information and file transfer history using this method. This will leave the product ready for [initial configuration](https://www.opswat.com/docs/netwalldiode/configuration/diode-initial-config).

Once in the CLI, execute the command **management** to access the list shown below:

Run the commands below to flush data and configuration:

## **Method 2 ( Complete re-image)**

Warning:

This method will completely erase the whole disk, including the OS. After running this command, the appliance will have to be rebuilt.

We recommend reaching out to OPSWAT Support before hand so you can gain access to the images and instructions you will need to rebuild the appliance.

To erase the whole disk, execute the following command via CLI.

After the command executes and completes, the appliance will be ready to be re-imaged again.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/support).

MetaDefender

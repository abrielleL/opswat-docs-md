<!-- source: https://www.opswat.com/docs/mdtransferguard/back-to-back-mode/back-to-back-mode -->

# Back to Back Mode

Back-to-Back MetaDefender Diode X requires two Diode X appliances that point in opposite directions. One Diode X is used to send data South-North and the other Diode X is used to send data North-South.

Info

Two Diode X appliances are required to configure Back-to-Back Mode.

The purpose of this feature is to utilize unidirectional existing TCP streams and allow any existing TCP connection to be split into ingress flow and egress flow. These flows are then routed via the appropriate Diode X in the Back-to-Back Diode set – in order to achieve normal TCP functionality.

Streams can work in two modes:

- Initiator
- Terminator

When in Initiator mode, it listens for incoming connections then forwards the ingress of the TCP stream to Diode 1’s BLUE configured unidirectional TCP Stream. The unidirectional TCP stream is “terminated” on the north instance of the Back-to-back Diode X.

Back-to-Back Diode concept

## [Back-to-Back Configuration](/docs/mdtransferguard/back-to-back-mode/back-to-back-mode#back-to-back-configuration)

Go to the Advanced menu and click on Back to Back Mode. Click on the Edit button.

Info

You will need to configure Back to Back Mode on both, BLUE and RED Servers and in both Diode X appliances.

Fill in the following fields:

- **Enabled:** Check box to enable Back to Back Mode.
- **Neighbor IP Address:** Management IP Address of the diode device setting in the same network as this appliance. In our example, if we are configuring 192.168.101.92, the neighbor would be 192.168.101.99.
- **Allow Initiating Back to Back Connections from this Netwall:** Allow Diode X users to create TCP/UDP Back to Back Streams that initiate the connection (called **Initiator**) from the Diode X. Both BLUE and RED sides need to have this enabled.
- **Network:** Select the network of the current Diode X and the defined neighbor.

Click on Submit button and repeat the same steps in the rest of Diode X appliances.

### [Configuring Initiator](/docs/mdtransferguard/back-to-back-mode/back-to-back-mode#configuring-initiator)

Once Back to Back Mode has been enabled and Neighbor IP Address is defined, the Initiator and Terminator Stream will be configured correctly.

When enabling Back to Back Mode, a new tab appears in the Streams section.

When a user defines an Initiator Stream, it will listen for incoming connections and split the single inbound connection into two streams, both bound to/from different MetaDefender Diode X instances.

A Terminator Stream will listen for incoming connection on the internal Diode X port and join the two streams between the correlated Back-to-Back Diode X instances – then send the normal TCP flow upstream to the designated server.

Info

When an Initiator Stream is created, it needs to be configured on both BLUE and RED.> > When a Terminator Stream is created, it needs to be configured on both BLUE and RED.

To configure an Initiator, go to Streams and click on the Back to Back Streams tab, click on Action and select Add TCP Back to Back Initiator or Add UDP Back to Back Initiator, then configure the Stream parameters.

#### [Diode X BLUE Configuration](/docs/mdtransferguard/back-to-back-mode/back-to-back-mode#diode-x-blue-configuration)

Complete the following:

- **Channel:** Assign a channel number.

Info

The channel number must be the same on both MetaDefender Transfer Guards as well as the BLUE and RED sides.

- **Type:** Type of stream being tracked. For adding an Initiator, this value will be preselected.
- **Name:** Name of the stream
- **Protocol:** select TCP or UDP depending on the stream you want to create. The value will be preselected depending on user's selection.
- **Source Port:** Port number of the source IP.
- **Source Addresses:** IP address(es) in the BLUE zone where the stream will originate. If you are entering more than one address, separate the addresses with a semicolon.
- **Enabled:** checkbox to enable/disable the stream.
- **Max Sessions:** Maximum number of sessions for the stream
- **Bitrate:** Maximum bitrate that BLUE side will reach for this stream. Users would need to tune this bitrate to avoid overload in the RED side.
- **Description:** user-friendly description.

#### [Diode X RED Configuration](/docs/mdtransferguard/back-to-back-mode/back-to-back-mode#diode-x-red-configuration)

Complete the following:

- **Channel:** Assign a channel number.

Info

The channel number needs to be the same on both the BLUE and RED sides.

- **Type:** Type of stream being tracked. For adding an Initiator, this value will be preselected.
- **Name:** Name of the stream
- **Protocol:** select TCP or UDP depending on the stream you want to create. The value will be preselected depending on user's selection.
- **Enabled:** checkbox to enable/disable the stream.
- **Max Buffer Items:** select the size of the buffer items queued on RED. For high speed streams, a larger buffer is preferred in order to avoid data overruns. Please, note that buffering data consumes memory.
- **Terminate on Failure:** This checkbox controls what happens in the event of data overrun. When the box is checked, the relevant connection on RED will be closed, all data buffers discarded and a new connection re-opened to allow for synchronization recovery. If left unchecked, the relevant connection remains intact and communication continues after the data buffers have been discarded.
- **Description:** user-friendly description.

### [Configuring Terminator](/docs/mdtransferguard/back-to-back-mode/back-to-back-mode#configuring-terminator)

To configure a Terminator go to Streams and click on the Back to Back Streams tab, click on Action and select Add TCP Back to Back Terminator or Add UDP Back to Back Terminator, then configure the Stream parameters.

#### [Diode X BLUE Configuration](/docs/mdtransferguard/back-to-back-mode/back-to-back-mode#diode-x-blue-configuration)

Complete the following:

- **Channel:** Assign a channel number.

Info

The channel number needs to be the same on both the BLUE and RED sides.

- **Type:** Type of stream being tracked. For adding a Terminator, this value will be preselected.
- **Name:** Name of the stream.
- **Protocol:** select TCP or UDP depending on the stream you want to create. The value will be preselected depending on user's selection.
- **Source Port:** Port number of the source IP.
- **Source Addresses:** IP address(es) in the BLUE zone where the stream will originate. If you are entering more than one address, separate the addresses with a semicolon.
- **Enabled:** checkbox to enable/disable the stream.
- **Max Sessions:** Maximum number of sessions for the stream.
- **Description:** user-friendly description.

#### [Diode X RED Configuration](/docs/mdtransferguard/back-to-back-mode/back-to-back-mode#diode-x-red-configuration)

Complete the following:

- **Channel:** Assign a channel number.

Info

The channel number needs to be the same on both the BLUE and RED sides.

- **Type:** Type of stream being tracked. For adding a Terminator, this value will be preselected.
- **Name:** Name of the stream
- **Protocol:** select TCP or UDP depending on the stream you want to create. The value will be preselected depending on user's selection.
- **Enabled:** checkbox to enable/disable the stream.
- **Max Buffer Items:** select the size of the buffer items queued on RED. For high speed streams, a larger buffer is preferred in order to avoid data overruns. Please, note that buffering data consumes memory.
- **Terminate on Failure:** This checkbox controls what happens in the event of data overrun. When the box is checked, the relevant connection on RED will be closed, all data buffers discarded and a new connection re-opened to allow for synchronization recovery. If left unchecked, the relevant connection remains intact and communication continues after the data buffers have been discarded.
- **Description:** user-friendly description.

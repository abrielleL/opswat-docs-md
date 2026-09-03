<!-- source: https://www.opswat.com/docs/supply-chain/operating/jfrog-binary -->

# JFrog

## How to configure Real Time Processing for JFrog Binary

In order to configure Real Time Processing in **MetaDefender Software Supply Chain** you will need to go to Inventory and click on a valid JFrog Binary service connection. There you can see a button that says **Start RTP**.

## Start a Real-Time Scan

- Go to **Inventory** and select your JFrog Binary service connection, then click **Start Job**:

![](https://uploads.developerhub.io/prod/jdK6/mb49utyvp8uos42p8xxz1b5xsz64ljis4ydylf8ij23key9c94c8j075ix6xmczc.png)

- In the New Job panel, select the repositories you want to monitor and switch to the **Real-Time Scan** tab. Choose a custom workflow - the **Webhook URL** is generated once the workflow is selected. Copy it, then click **Create**:

![](https://uploads.developerhub.io/prod/jdK6/6i25pfhzs0e7a0tqdjxtos3zp1fdnvputz4pw2j05j2i3dvggxf1bvfr32cegu9k.png)

- - The Real-Time job appears in the **Active Jobs** table on the Jobs page and keeps running while the repositories are monitored:

![](https://uploads.developerhub.io/prod/jdK6/v9nrp73c3g0ksrns10wj1pqlynde99v837q0fswvevnxctd0rpqooebsipv5gb7i.png)

## How to use Webhooks

1. Go to your **JFrog instance** → Administration → General Management → Webhooks → New Webhook

![](https://uploads.developerhub.io/prod/jdK6/vvmnyifro2pg5xyxwz1hgvpf7v0nq1nf62inopkzlje8aiiqzkx77p87iv3s1fv7.png)

2. Fill the necessary details by giving a name, the **URL** will be the generated URL from **MetaDefender Software Supply Chain**, select a compatible **event type** (in this example, we use `copy artifact event` ) and also add a custom header including the API Key:

**Note:** For **JFrog Container** connections, we currently support the `Docker and OCI -> Tag was pushed` event type.

![](https://uploads.developerhub.io/prod/jdK6/97duihtz1bn4cf2b75ndknlqlt631nhnzzoh897fxi2ydqmqzq8j4p40i33osgsn.png)

![](https://uploads.developerhub.io/prod/jdK6/2pkxsojkrdz12xl039vsv0vsn8tquhxqoynofeg4pur75yayaxa570ish5pyhqaw.png)

3. When you add an event, a form from which to choose the repositories will appear. Here, choose the one which you generated the webhook from:

![](https://uploads.developerhub.io/prod/jdK6/xiexbje6lwn1d72fja4flxx0t11acn5u9rmyve0mr5390gez3621d86pzgljhfrc.png)

4. After everything is settled, click `Create` and the new webhook will be added to the list:

![](https://uploads.developerhub.io/prod/jdK6/undgukw3jfjwx29v57obslnsf07whenex0lt5juyuamwr2ycp71lg3m490bzdaav.png)

Now, when an artifact is copied into the selected repo, a scan will be automatically triggered.

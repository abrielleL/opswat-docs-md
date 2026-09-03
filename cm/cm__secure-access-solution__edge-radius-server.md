<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/edge-radius-server -->

# Edge Radius Server

Edges are on-premise components that communicate directly with network devices to enforce policies, while simultaneously receiving configuration updates from the Cloud. These components can be deployed across multiple sites, with their status displayed on the My OPSWAT Central Management portal.

### Create Edge RADIUS Server

1. Login to your **My OPSWAT Central Management**
2. Navigate to **RADIUS NAC**
3. Click on **Add Edge RADIUS Server**
4. Fill in your **Edge Server** name
5. Upon create successfully, an associate API Key will be generated. Later, that API Key will be used to setup the NAC VM

![](https://uploads.developerhub.io/prod/6Ad9/g7pkyuf7prl9zkrnvgcjayzxu7sc8dm03cw8f173vulz58qgwobkstja8vf578mj.png)

**Note**: Each NAC Edge can integrate with only **one Virtual Machine (VM)**. If you are deploying multiple NAC Edges across your network, each Edge will require a dedicated VM for integration. This ensures proper functioning and enforcement of security policies for each site.

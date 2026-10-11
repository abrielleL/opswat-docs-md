<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/data-trickling -->

# Data Trickling

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdicap/v5.14.1/integrations/data-trickling#overview)

Blue Coat ProxySG appliances implement Data Trickling to improve the user experience during ICAP scanning. Internet Content Adaptation Protocol (ICAP) is the protocol used by Blue Coat ProxySG and ProxyAV appliances, as well as some third party partner appliances, to perform scanning of objects to detect viruses, worms, spyware, and Trojans. Data Trickling is a mechanism implemented by Blue Coat ProxySG appliances performing ICAP scanning that slowly delivers, or trickles, data to the client as it is being scanned. By trickling data, users do not experience the timeouts sometimes associated with waiting for large objects to be scanned, or when scanning is delayed by high loads on content servers or upstream bandwidth limitations.

## [How does Data Trickling work?](/docs/mdicap/v5.14.1/integrations/data-trickling#how-does-data-trickling-work)

Data Trickling is designed to prevent the timeouts that can sometimes be associated with patience pages. To prevent such timeouts, Data Trickling trickles – or transmits at a very slow rate – bytes to the client at the beginning of the scan or near the very end. Because the ProxySG appliance begins serving content without waiting for the ICAP scan result, timeouts do not occur. However, to maintain security, the full object is not delivered until the results of the content scan are complete (and the object is determined to not be infected). Two types of Data Trickling are available on Blue Coat ProxySG appliances – trickle from start and trickle at end.

## [Trickle from start](/docs/mdicap/v5.14.1/integrations/data-trickling#trickle-from-start)

In trickle from start mode, the ProxySG appliance buffers a small amount of the beginning of the response body. As the ICAP server continues to scan the response, the ProxySG appliance allows one byte per second to the client. After the ICAP server completes its scan, if the object is deemed to be clean (no response modification is required), the ProxySG appliance sends the rest of the object bytes to the client at the best speed allowed by the connection. If the object is deemed to be malicious, the ProxySG appliance terminates the connection and the remainder of the response object. Trickling from the start is the more secure Data Trickling option because the client receives only a small amount of data pending the outcome of the virus scan.

## [Trickle at end](/docs/mdicap/v5.14.1/integrations/data-trickling#trickle-at-end)

In trickle at end mode, the ProxySG appliance sends the response to the client at the best speed allowed by the connection, except for the last 16KB of data. As the ICAP server performs the content scan, the ProxySG appliance allows one byte per second to the client. After the ICAP server completes its scan, if the object is deemed to be clean (no response modification is required), the ProxySG appliance sends the rest of the object bytes to the client at the best speed allowed by the connection. This method is more user-friendly than trickle at start. This is because users tend to be more patient when they notice that 99% of the object is downloaded versus 1%, and are less likely to perform a connection restart. However, network administrators might perceive this method as the less secure method, as a majority of the object is delivered before the results of the ICAP scan.

## [Step-by-step guide](/docs/mdicap/v5.14.1/integrations/data-trickling#step-by-step-guide)

To enable data trickling:

1. Open the BlueCoat Management Console.
2. Go to "Configuration" tab > "Advanced configuration" button.
3. Enter credentials if prompted.
4. In the Advanced configuration menu, go to "Configuration" tab > "External Services" > "ICAP".
5. Click the "ICAP Feedback" tab.
6. In the "ICAP Feedback for Interactive Traffic" section:

   1. Check "Provide feedback after X seconds" checkbox
   2. Set the number of seconds to the time you want to wait for ICAP to respond before starting trickling

      - 8 seconds is a usually a good timing, long enough for average file sizes to be fully scanned by ICAP, short enough for browsers to not timeout before trickling starts.
   3. Check the "Trickle object data from start" or "Trickle object data at end" depending on the trickling type you want (see "How does Data Trickling work" section).

      - "From start" is the most secure.
      - "At end" is the most user friendly.
7. In the "ICAP Feedback for Non-Interactive Traffic" section:

   1. Check "Provide feedback after X seconds" checkbox
   2. Set the number of seconds to the time you want to wait for ICAP to respond before starting trickling

      - 5 seconds is a usually a good timing for non-interactive traffic
   3. Check the "Trickle object data from start" or "Trickle object data at end" depending on the trickling type you want (see "How does Data Trickling work" section).

      - "From start" is the most secure.
      - "At end" is the most user friendly.

## [More info](/docs/mdicap/v5.14.1/integrations/data-trickling#more-info)

<https://www.bluecoat.com/sites/default/files/documents/files/ICAP_Data_Trickling.7.pdf>

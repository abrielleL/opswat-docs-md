<!-- source: https://www.opswat.com/docs/mdcloud/knowledge-base/how-do-i-export-metadefender-cloud-scan-history-as-csv- -->

# How do I export MetaDefender Cloud scan history as CSV?

This article applies to all active MetaDefender Cloud license holders - whether your product is paid for or issued for evaluation purposes. For more information on our range of licensing and evaluation options, please [Read This](https://metadefender.opswat.com/licensing).

While it is possible to export individual scan results as PDF file on MetaDefender Cloud web interface, the option to export scan history as JSON or CSV isn’t available on the web interface.

However, you can call the API endpoint [GET /apikey/scan-history](https://www.opswat.com/docs/mdcloud/metadefender-cloud-api-v4#getapikey-scan-history) to retrieve scan history as a JSON file and utilize a script to convert the JSON response to a CSV file.

- If you want to scan history in JSON format, simply save the response to a file.

Below is an example Python script to call this API endpoint and convert the response to a CSV file:

- In this example, the header “apikey” and the parameters “limit”, “offset” are hardcoded, but you should use environment variables to set these values.
- The “api_url” has the parameters “limit” and “offset”, which determine how many entries you want to return, and how many entries to skip (sorted chronologically). In this example, “limit=10” and “offset=0” will return the latest 10 entries in scan history.

Python script: scan-history-csv.py

PythonCopyimport requests
import pandas as pd
# API URL and headers
api_url = "https://api.metadefender.com/v4/apikey/scan-history?limit=10&offset=0"
headers = {
'apikey': '<mdcloud_api_key>',
'Accept': 'application/json; charset=utf-8'
}
# Fetch the JSON data from the API
response = requests.get(api_url, headers=headers)
data = response.json()
# Convert JSON data to a DataFrame
df = pd.DataFrame(data['data']) # Adjust the key based on the actual JSON structure
# Save DataFrame to a CSV file
df.to_csv("scan_history.csv", index=False)
print("JSON data has been converted to scan_history.csv")

Running the script will produce the following output, and “scan_history.csv” file in the same directory:

PowershellCopyPS > python scan-history-csv.py
JSON data has been converted to scan_history.csv

Example CSV file output:

This is only a basic example of how such a script will function, so feel free to customize it to suit your needs.

Support:

For queries and concerns on **How to export MD Cloud scan history as CSV**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).

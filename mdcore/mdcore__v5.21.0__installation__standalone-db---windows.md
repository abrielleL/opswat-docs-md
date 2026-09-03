<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/installation/standalone-db---windows -->

# Standalone DB - Windows

These results should be viewed as guidelines and not performance guarantees, since there are many variables that affect performance (file set, network configurations, hardware characteristics, etc.). If throughput is important to your implementation, OPSWAT recommends site-specific benchmarking before implementing a production solution.

## [Environment](/docs/mdcore/v5.21.0/installation/standalone-db---windows#environment)

Using AWS environment with the specification below:

### [MetaDefender Core](/docs/mdcore/v5.21.0/installation/standalone-db---windows#metadefender-core)

| OS | AWS instance type | vCPU | Memory (GB) | Network bandwidth (Gbps) | Disk type | Benchmark |
| --- | --- | --- | --- | --- | --- | --- |
| Windows Server 2022 | c5a.8xlarge | 32 | 64 | Up to 10 | SSD | [Amazon EC2 c5a.8xlarge - Geekbench](https://browser.geekbench.com/v6/cpu/10078683) |

### [Client tool](/docs/mdcore/v5.21.0/installation/standalone-db---windows#client-tool)

A simple tool written in Python to collect files in a designated folder and submit requests to MetaDefender Core.

This client tool is running on CentOS 7

PythonCopyfiles_to_scan = list of files to scan
scan_futures = [asyncio.create_task(self.scan_file(file_path)) for file_path in files_to_scan]
async def scan_file(self, file_path):
api_url = f'{self.core_url}/file'
with open(file_path, 'rb') as file:
file_content = file.read()
headers = {'Content-Type': 'application/octet-stream', 'filename': file_path}
max_retries = 20 # Maximum number of retry attempts
retry_delay = 120 # Delay in seconds before retrying
for attempt in range(max_retries + 1):
try:
response = requests.post(api_url, data=file_content, headers=headers)
status_code = response.status_code
if status_code == 200:
response_json = response.json()
data_id = response_json.get('data_id')
return status_code, response_json, data_id
if status_code == 503:
print(f"Received status code {status_code}. Retrying in {retry_delay} seconds...")
await asyncio.sleep(retry_delay)
else:
return None, None, None
except requests.RequestException as e:
return None, None, None
return None, None, None

| OS | AWS instance type | vCPU | Memory (GB) | Network bandwidth (Gbps) | Disk type |
| --- | --- | --- | --- | --- | --- |
| CentOS 7 | c5.4xlarge | 16 | 32 | Up to 10 | SSD |

## [Dataset](/docs/mdcore/v5.21.0/installation/standalone-db---windows#dataset)

Detailed information of dataset below will be used for testing:

| File category | File type | Number of files | Total size (MB) | Average file size (MB) |
| --- | --- | --- | --- | --- |
| Adobe | PDF | 370 | 385 MB | 1.0 MB |
| Executable | EXE | 45 | 309.5 MB | 6.9 MB |
|  | MSI | 15 | 45.75 MB | 3.1 MB |
| Image | BMP | 80 | 515 MB | 6.4 MB |
|  | JPG | 420 | 237.5 MB | 0.6 MB |
|  | PNG | 345 | 169 MB | 0.5 MB |
| Media | MP3 | 135 | 865 MB | 6.4 MB |
|  | MP4 | 50 | 500 MB | 10.0 MB |
| Office | DOCX | 235 | 190 MB | 0.8 MB |
|  | DOC | 225 | 486 MB | 2.2 MB |
|  | PPTX | 365 | 860 MB | 2.4 MB |
|  | PPT | 355 | 1950 MB | 5.5 MB |
|  | XLSX | 340 | 283.5 MB | 0.8 MB |
|  | XLS | 335 | 284.5 MB | 0.8 MB |
| Text | CSV | 100 | 236 MB | 2.4 MB |
|  | HTML | 1075 | 76 MB | 0.1 MB |
|  | TXT | 500 | 210 MB | 0.4 MB |
| Archive | ZIP | Compressed files: 10  Extracted files: 270 | Compressed size: 125.5 MB  Extracted size: 156.5 MB | Avg compressed size: 12.6 MB  Avg extracted size: 0.6 MB |
| **Summary (compressed)** |  | 5000 | 7728.5 MB | 1.55 MB average file size |
| **Summary (extracted)** |  | 5260 | 7759.5 MB | 1.48 MB average file size |

## [Product Information](/docs/mdcore/v5.21.0/installation/standalone-db---windows#product-information)

Product versions:

- MetaDefender Core 5.21.0
- Engines:

  - Metascan 8: Ahnlab, Avira, ClamAV, ESET, Bitdefender, K7, Quick Heal, VirIT Explorer
  - Metascan 12: Metascan 8, Varist, Ikarus, Emsisoft, Tachyon
  - Metascan 16: Metascan 12, Bkav Pro, CMC, Xcitium, Zillya!
  - Deep CDR: 8.0.1
  - Proactive DLP: 3.4.0
  - Archive: 8.0.2
  - File type analysis: 8.0.2
  - File-based vulnerability assessment: 4.2.416.0
  - Adaptive Sandbox: 3.2.0

## [MetaDefender Core settings](/docs/mdcore/v5.21.0/installation/standalone-db---windows#metadefender-core-settings)

### [General settings](/docs/mdcore/v5.21.0/installation/standalone-db---windows#general-settings)

- Turn off data retention
- Turn off engine update
- Max file size: 99999999

### [Archive extraction settings](/docs/mdcore/v5.21.0/installation/standalone-db---windows#archive-extraction-settings)

- Max recursion level: 99999999
- Max number of extracted files: 99999999
- Max total size of extracted files: 99999999
- Timeout: 10 minutes
- Handle archive extraction task as Failed: true

  - Extracted partially: true

### [Metascan AV settings](/docs/mdcore/v5.21.0/installation/standalone-db---windows#metascan-av-settings)

- Scan timeout: 10 minutes
- Per engine scan timeout: 1 minutes

### [Adaptive Sandbox](/docs/mdcore/v5.21.0/installation/standalone-db---windows#adaptive-sandbox)

- Max file size: 18446744073709 MB (max)
- Timeout: 86400 (max)

## [Performance test results](/docs/mdcore/v5.21.0/installation/standalone-db---windows#performance-test-results)

### [Summary](/docs/mdcore/v5.21.0/installation/standalone-db---windows#summary)

**MetaDefender Core with single engine (technology):**

**MetaDefender Core with common engine packages:**

### [System resource utilization charts](/docs/mdcore/v5.21.0/installation/standalone-db---windows#system-resource-utilization-charts)

**MetaDefender Core with Metascan 8 + Deep CDR + Proactive DLP + Vulnerability + Sandbox:**

|  | Utilization charts |
| --- | --- |
| **CPU usage** |  |
| **Memory usage** |  |
| **Network usage** |  |
| **Disk usage** |  |

**MetaDefender Core with Metascan 16 + Deep CDR + Proactive DLP + Vulnerability + Sandbox:**

|  | Utilization charts |
| --- | --- |
| **CPU usage** |  |
| **Memory usage** |  |
| **Network usage** |  |
| **Disk usage** |  |

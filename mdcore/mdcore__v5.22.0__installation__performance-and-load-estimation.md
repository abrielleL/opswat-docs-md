<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/installation/performance-and-load-estimation -->

# Performance and Load Estimation

These results should be viewed as guidelines and not performance guarantees, since there are many variables that affect performance (file set, network configurations, hardware characteristics, etc.). If throughput is important to your implementation, OPSWAT recommends site-specific benchmarking before implementing a production solution.

## [Some factors that affect performance](/docs/mdcore/v5.22.0/installation/performance-and-load-estimation#some-factors-that-affect-performance)

- MetaDefender Core version
- MetaDefender Core engine package and configuration

  - set of engines (which and how many)
  - product configuration (e.g., thread pool size)
- System environment

  - server profile (CPU, RAM, hard disk)
  - client application location - remote or local
  - system caching and engine level caching
- Dataset

  - encrypted or decrypted
  - file types

    - different file types (e.g., document, image, executable)
    - archive file or compound document format files
  - file size
  - bad or unknown (assume to be clean)
- Performance tool

## [How test results are calculated](/docs/mdcore/v5.22.0/installation/performance-and-load-estimation#how-test-results-are-calculated)

Performance (mainly scanning speed) is measured by throughput rather than unit speed. For example, if it takes 10 seconds to process 1 file, and it also takes 10 seconds to process 10 files, then performance is quantified as 1 second per file, rather than 10 seconds.

- total time / total number of files processed: 10 seconds / 10 files = 1 second / file.

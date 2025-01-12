
# `pt-diskstats` — A Percona Toolkit Tool for Disk I/O Analysis

## Overview
`pt-diskstats` is a command-line tool from **Percona Toolkit** designed to retrieve and analyze disk I/O statistics from your Linux system. By examining system performance metrics related to disk usage, you can assess how well your system's disks are performing and identify potential bottlenecks.

This tool provides insights into disk I/O activity and assists with troubleshooting issues related to disk throughput, latency, and other disk-related performance factors.

---

## Features
- **Disk Usage Statistics**: Collects real-time disk I/O statistics.
- **Aggregated Data**: Provides aggregated metrics such as read and write operations, sectors read and written, and I/O times.
- **Multiple Output Options**: Offers customizable output formats for easy integration with other tools or systems.
- **Multiple Device Support**: Supports analyzing multiple disks on your system simultaneously.

---

## Installation

To use `pt-diskstats`, you'll need to have Percona Toolkit installed. If you haven't already, follow the steps below:

### On Ubuntu/Debian
```bash
sudo apt-get update
sudo apt-get install percona-toolkit
```

### On CentOS/RHEL
```bash
sudo yum install percona-toolkit
```

## Usage
The basic syntax for running pt-diskstats is:

```bash
pt-diskstats [OPTIONS]
```

### Common Options
- `--interval`: Specifies the time interval between each statistics report (e.g., `--interval=1s` for 1-second intervals).
- `--disk`: Limits the output to a specific disk device (e.g., `/dev/sda`).
- `--daemon`: Runs pt-diskstats as a daemon, continuously collecting disk statistics.
- `--help`: Displays help information about the command and its options.

### Examples
- Basic usage to show disk I/O statistics:
  ```bash
  pt-diskstats
  ```

- Monitor I/O statistics every 5 seconds:
  ```bash
  pt-diskstats --interval=5s
  ```

- Monitor a specific disk device:
  ```bash
  pt-diskstats --disk=/dev/sda
  ```

## Output Explanation

Example output:

```text
# ts device       rd_s  rd_avkb  rd_mb_s  rd_mrg  rd_cnc   rd_rt    wr_s  wr_avkb  wr_mb_s  wr_mrg  wr_cnc   wr_rt  busy  in_prg   io_s  qtime  stime
1.  sda          1500   32.0     48.0     5.0     3.0     0.5     2000   64.0     128.0    4.0     2.0     0.8   20.0   1        0.2   0.1    0.4
1.  sdb          800    16.0     32.0     3.0     2.0     0.3     1200   32.0     64.0     2.0     1.0     0.4   15.0   0        0.1   0.0    0.3
1.  nvme0n1     3000   128.0    256.0    10.0    5.0     0.7     5000   256.0    512.0    8.0     4.0     1.2   30.0   2        0.4   0.2    0.6
```

Explanation of Columns:
- `ts`: Timestamp of the data collection.
- `device`: The disk device identifier.
- `rd_s`: Number of read requests.
- `rd_avkb`: Average read size in kilobytes.
- `rd_mb_s`: Read speed in megabytes per second.
- `rd_mrg`: Number of read merges.
- `rd_cnc`: Number of read requests completed.
- `rd_rt`: Average read response time in milliseconds.
- `wr_s`: Number of write requests.
- `wr_avkb`: Average write size in kilobytes.
- `wr_mb_s`: Write speed in megabytes per second.
- `wr_mrg`: Number of write merges.
- `wr_cnc`: Number of write requests completed.
- `wr_rt`: Average write response time in milliseconds.
- `busy`: Percentage of time the device was busy.
- `in_prg`: Number of I/O operations in progress.
- `io_s`: I/O operations per second.
- `qtime`: Average queue time for requests.
- `stime`: Average service time for requests.

---

## Advanced Features

### Daemon Mode
To continuously monitor disk statistics, you can run pt-diskstats as a background daemon:

```bash
pt-diskstats --daemon --interval=10s
```

This will collect disk statistics every 10 seconds and output them to a file.

### Output to a File
To store disk statistics in a log file for later analysis:

```bash
pt-diskstats --interval=1s > diskstats.log
```

### Output Format Customization
You can customize the output format to suit your needs using various options. For example, using the `--format` flag allows you to choose the type of output:

```bash
pt-diskstats --format=csv
```

This will output the data in CSV format for easier analysis.

---

## Troubleshooting

### Common Issues

- **Permission Denied**:  
  If you encounter a permission denied error, ensure you're running the command as a user with the necessary privileges (typically root or a user with appropriate sudo privileges).
  ```bash
  sudo pt-diskstats
  ```

- **Missing Disk Devices**:  
  If a specific disk is not showing in the output, ensure the device exists and is correctly mounted. You can check the available devices using `lsblk`.

---

## Requirements
- **Linux**: pt-diskstats is designed to run on Linux systems.
- **Percona Toolkit**: Ensure you have the Percona Toolkit installed, which includes the pt-diskstats tool.
- **Root Privileges**: Some functionality may require root access to collect certain system statistics.

## License
pt-diskstats is part of the Percona Toolkit, which is licensed under the GPL-2.0 License.

---

## Additional Resources
For more information, visit the [Percona Toolkit Documentation](https://www.percona.com/doc/percona-toolkit).
```

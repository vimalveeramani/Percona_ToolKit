
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

---

## Usage

The basic syntax for running `pt-diskstats` is:

```bash
pt-diskstats [OPTIONS]
```

### Common Options
- `--interval`: Specifies the time interval between each statistics report (e.g., `--interval=1s` for 1-second intervals).
- `--disk`: Limits the output to a specific disk device (e.g., `/dev/sda`).
- `--daemon`: Runs `pt-diskstats` as a daemon, continuously collecting disk statistics.
- `--help`: Displays help information about the command and its options.

### Examples

1. **Basic usage to show disk I/O statistics**:
    ```bash
    pt-diskstats
    ```

2. **Monitor I/O statistics every 5 seconds**:
    ```bash
    pt-diskstats --interval=5s
    ```

3. **Monitor a specific disk device**:
    ```bash
    pt-diskstats --disk=/dev/sda
    ```

---

## Output Explanation

`pt-diskstats` produces detailed statistics related to disk performance. Below is an example of the typical output:

```
Device   Reads  Writes  Read-Sectors  Write-Sectors  Read-IOs  Write-IOs  Time-Read-IOs  Time-Write-IOs
/dev/sda 1500   2000    1500000       2000000        2.3      4.5        0.2            0.3
```

**Columns**:
- `Device`: The disk device being analyzed.
- `Reads`: The number of read operations performed.
- `Writes`: The number of write operations performed.
- `Read-Sectors`: The total number of sectors read.
- `Write-Sectors`: The total number of sectors written.
- `Read-IOs`: The time taken for read I/O operations.
- `Write-IOs`: The time taken for write I/O operations.
- `Time-Read-IOs`: The average time spent on read I/O operations.
- `Time-Write-IOs`: The average time spent on write I/O operations.

---

## Advanced Features

### Daemon Mode
To continuously monitor disk statistics, you can run `pt-diskstats` as a background daemon:

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

1. **Permission Denied**:
    If you encounter a permission denied error, ensure you're running the command as a user with the necessary privileges (typically root or a user with appropriate sudo privileges).

    ```bash
    sudo pt-diskstats
    ```

2. **Missing Disk Devices**:
    If a specific disk is not showing in the output, ensure the device exists and is correctly mounted. You can check the available devices using `lsblk`.

---

## Requirements

- **Linux**: `pt-diskstats` is designed to run on Linux systems.
- **Percona Toolkit**: Ensure you have the Percona Toolkit installed, which includes the `pt-diskstats` tool.
- **Root Privileges**: Some functionality may require root access to collect certain system statistics.

---

## License

`pt-diskstats` is part of the Percona Toolkit, which is licensed under the **GPL-2.0 License**.

---


## Additional Resources

For more information, visit the [Percona Toolkit Documentation](https://www.percona.com/doc/percona-toolkit/).

---


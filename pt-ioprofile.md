# pt-ioprofile

`pt-ioprofile` is a tool from Percona Toolkit that captures real-time I/O operations performed by a process. It helps database administrators analyze disk activity and troubleshoot performance bottlenecks in MySQL and other applications.

## Features
- Monitors system calls related to file I/O in real-time.
- Helps identify slow queries causing excessive disk activity.
- Works with any process, including MySQL and PostgreSQL.
- Provides insights into read/write patterns and potential optimizations.

## Installation
To install Percona Toolkit, including `pt-ioprofile`, use:
```sh
# On Debian/Ubuntu
sudo apt-get install percona-toolkit

# On RHEL/CentOS
sudo yum install percona-toolkit

# Using Homebrew (MacOS)
brew install percona-toolkit
```

## Usage
### Basic Command
```sh
pt-ioprofile --pid=<process_id>
```

### Example
```sh
pt-ioprofile --pid=1234
```

### Common Options
| Option | Description |
|--------|-------------|
| `--pid` | Process ID to monitor. |
| `--duration` | Time duration (in seconds) to capture I/O activity. |
| `--output` | Specify an output file for logging results. |

## Interpreting Output
The output provides details such as:
- Read/write operations count
- File descriptors accessed
- Latency of disk operations

Example output:
```
FILE                    READS  WRITES  READ_BYTES  WRITE_BYTES
/var/lib/mysql/db.ibd    100    50      204800      102400
/var/log/mysql.log        30    10       51200       10240
```

## Best Practices
- Use `pt-ioprofile` during peak load times to analyze disk performance.
- Combine this tool with `EXPLAIN ANALYZE` for deeper query optimization.
- Monitor trends over time to detect unusual disk activity patterns.

## Documentation
For detailed usage and additional options, visit the official documentation:
[Percona Toolkit - pt-ioprofile](https://docs.percona.com/percona-toolkit/pt-ioprofile.html)

## License
Percona Toolkit is licensed under the [GNU General Public License (GPL)](https://www.gnu.org/licenses/gpl-3.0.html).

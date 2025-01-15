
# Percona Toolkit: pt-kill

`pt-kill` is a powerful command-line tool from Percona Toolkit designed to automatically kill MySQL queries that meet specific conditions. It's especially useful for terminating long-running or resource-intensive queries to help maintain database performance. You can set time limits, query patterns, and even configure custom rules for when queries should be killed.

## Installation

Ensure that Percona Toolkit is installed before using `pt-kill`. Use the following methods to install it:

### On Linux (Ubuntu/Debian)
```bash
sudo apt-get install percona-toolkit
```

### On CentOS/RHEL
```bash
sudo yum install percona-toolkit
```

### Using Homebrew (macOS)
```bash
brew install percona-toolkit
```

For more installation details, see the official [Percona Toolkit Installation Guide](https://www.percona.com/doc/percona-toolkit/).

## Usage

```bash
pt-kill [OPTIONS]
```

### Required Options
- `--host`: The MySQL server hostname or IP address.
- `--user`: The MySQL user.
- `--password`: The MySQL user password.

### Common Options
- `--interval`: Specifies the interval (in seconds) between checking queries (default is 1 second).
- `--long-query-time`: Defines the threshold (in seconds) for queries to be considered long-running and eligible for termination.
- `--kill`: Automatically kill the long-running queries that match the conditions.
- `--where`: Allows you to filter queries based on specific conditions, such as query content or execution time.

## Example Usage

### 1. Kill Queries Running Longer than 60 Seconds
This command will monitor queries running for more than 60 seconds and automatically kill them.

```bash
pt-kill --host=localhost --user=root --password=yourpassword --long-query-time=60 --kill
```

### 2. Kill Specific Queries Matching a Pattern
If you want to terminate all queries that involve `UPDATE` operations and run longer than 5 seconds, you can specify a pattern and a time limit like this:

```bash
pt-kill --host=localhost --user=root --password=yourpassword --long-query-time=5 --where 'command="Query" AND info LIKE "UPDATE%"' --kill
```

### 3. Monitor and Kill Queries with a Custom Interval
You can also adjust the interval at which the tool checks for long-running queries. For instance, to kill any query running for over 120 seconds, with a check every 5 seconds:

```bash
pt-kill --host=localhost --user=root --password=yourpassword --long-query-time=120 --interval=5 --kill
```

### 4. Dry Run (Preview Queries That Would Be Killed)
You can preview which queries would be killed without actually terminating them by omitting the `--kill` flag:

```bash
pt-kill --host=localhost --user=root --password=yourpassword --long-query-time=30
```

This command will list all queries longer than 30 seconds that would be terminated, without actually killing them.

## Output

If the `--kill` option is used, `pt-kill` will output a confirmation message for each query it kills. If you choose the dry-run method, it will simply show you the queries that meet your specified conditions.

Example output:

```
Query id 12345 (Thread id 100) was running for 70 seconds, killing it now.
Query id 12346 (Thread id 101) was running for 180 seconds, killing it now.
```

## Conclusion

`pt-kill` is an effective tool for automating the termination of long-running or problematic queries in MySQL databases. It helps keep your system performance in check by eliminating queries that could negatively impact your server’s resources. The tool provides various customization options, such as filtering queries by patterns or controlling the kill interval.

For more advanced configurations, you can refer to the official [Percona Toolkit documentation](https://docs.percona.com/percona-toolkit/pt-kill.html).

---


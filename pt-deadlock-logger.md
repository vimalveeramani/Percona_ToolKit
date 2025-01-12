
# pt-deadlock-logger

`pt-deadlock-logger` is a tool from Percona Toolkit designed to monitor and log MySQL deadlocks by parsing the output of `SHOW ENGINE INNODB STATUS`. It captures new deadlocks and outputs them to `STDOUT` or stores them in a specified database table for further analysis.

## Usage

```bash
pt-deadlock-logger [OPTIONS] DSN
```

- **DSN**: Data Source Name specifying the database connection parameters.

### Examples

- Print deadlocks on `host1`:

  ```bash
  pt-deadlock-logger h=host1
  ```

- Print deadlocks on `host1` once and then exit:

  ```bash
  pt-deadlock-logger h=host1 --iterations 1
  ```

- Save deadlocks from `host1` to `percona_schema.deadlocks` on `host2`:

  ```bash
  pt-deadlock-logger h=host1 --dest h=host2,D=percona_schema,t=deadlocks
  ```

## Options

- `--dest`: DSN specifying where to store detected deadlocks.
- `--iterations`: Number of iterations to run before exiting.
- `--run-time`: Total time to run before exiting.
- `--quiet`: Suppress output to `STDOUT`.
- `--columns`: Specify which columns to include in the output.
- `--tab`: Output columns separated by a tab character.

## Output

By default, new deadlocks are printed to `STDOUT`. If the `--dest` option is specified, the tool uses `INSERT IGNORE` to store deadlock information in the designated table, preventing duplicate entries.

### Output Columns

When deadlocks are detected, `pt-deadlock-logger` captures the following information:

| Column          | Description |
|----------------|-------------|
| `ts`           | Timestamp when the deadlock occurred. |
| `server`       | Hostname of the MySQL server where the deadlock was detected. |
| `thread`       | Thread ID involved in the deadlock. |
| `txn_id`       | Transaction ID of the deadlocked transaction. |
| `txn_time`     | Time (in seconds) the transaction had been running before the deadlock. |
| `user`         | MySQL user executing the transaction. |
| `hostname`     | Hostname or IP address of the client that initiated the transaction. |
| `ip`           | IP address of the client (if available). |
| `db`           | Database name where the deadlock occurred. |
| `tbl`          | Table name involved in the deadlock. |
| `idx`          | Index name used in the deadlocked query. |
| `lock_type`    | Type of lock involved in the deadlock. |
| `waiting`      | Whether the transaction was waiting for a lock (`YES` or `NO`). |
| `victim`       | Whether this transaction was selected as the deadlock victim (`YES` or `NO`). |
| `query`        | The SQL query that was executing when the deadlock occurred. |

### Example Output

When a deadlock occurs, `pt-deadlock-logger` captures the information and displays it in a structured format:

```
# 2025-01-12T10:05:30
server: mysql-prod-1
thread: 12345
txn_id: 456789
txn_time: 10
user: app_user
hostname: app-server-1
ip: 192.168.1.10
db: orders_db
tbl: orders
idx: order_idx
lock_type: RECORD
waiting: YES
victim: NO
query: UPDATE orders SET status='shipped' WHERE id=123
```

If configured with `--dest`, this data will be stored in a MySQL table.

## InnoDB Caveats

InnoDB's deadlock information may sometimes be incomplete, lacking details such as username or IP address. In such cases, the tool can only log the available information.

## Risks

While `pt-deadlock-logger` is a mature and well-tested tool, it's essential to:

- Read the tool’s documentation thoroughly.
- Test the tool in a non-production environment.
- Ensure you have recent backups of your production database.

## Downloading

You can download the latest release of Percona Toolkit from the official website:

```bash
wget percona.com/get/percona-toolkit.tar.gz
```

Alternatively, for Debian-based systems, you can use:

```bash
wget percona.com/get/percona-toolkit.deb
```

For RPM-based systems:

```bash
wget percona.com/get/percona-toolkit.rpm
```

## Authors

- Baron Schwartz
- Daniel Nichter

## About Percona Toolkit

Percona Toolkit is a collection of advanced command-line tools for MySQL, developed by Percona. It was forked from Maatkit and Aspersa in June 2011. For more information, visit the [Percona software page](http://www.percona.com/software/).

## License

This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License version 2 or the Perl Artistic License. For more details, refer to the licenses provided with the program.

## Version

`pt-deadlock-logger` version: 3.6.0

*Note: This documentation is based on the information available as of January 12, 2025. For the most current details, please refer to the official Percona Toolkit documentation.*

```

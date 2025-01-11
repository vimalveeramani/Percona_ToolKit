
# pt-align - Percona Toolkit for Table Alignment

`pt-align` is a utility from **Percona Toolkit** designed to optimize and align tables in MySQL or MariaDB. It helps fix table fragmentation, which can occur when rows are inserted and deleted over time, leading to performance issues. By realigning the table, the utility ensures that physical storage is optimized.

## Prerequisites

- **Percona Toolkit** must be installed. You can install it via package managers or from source.
- The MySQL/MariaDB user running the tool must have sufficient privileges (`ALTER`, `DROP`, `INSERT`, and `SELECT`).

## Installation

You can install Percona Toolkit on Linux by using the following commands:

### On Ubuntu/Debian:
```bash
sudo apt-get update
sudo apt-get install percona-toolkit
```

### On CentOS/RHEL:
```bash
sudo yum install percona-toolkit
```

## Usage

### Basic Command

The basic syntax of `pt-align` is:

```bash
pt-align --host=<hostname> --user=<username> --password=<password> --database=<database> --table=<table>
```

### Parameters

- `--host` (Required): The MySQL server host (e.g., `localhost`).
- `--user` (Required): The MySQL user.
- `--password` (Required): The MySQL user password.
- `--database` (Required): The database to perform the operation on.
- `--table` (Required): The specific table to align (e.g., `orders`).
- `--dry-run` (Optional): Performs a dry run to preview changes without making modifications.

### Example

To align the `orders` table in the `shop_db` database:

```bash
pt-align --host=localhost --user=root --password=mysecretpassword --database=shop_db --table=orders
```

This will optimize the `orders` table on the MySQL server running on `localhost`.

### Dry Run Example

To simulate the operation without making any changes, use the `--dry-run` option:

```bash
pt-align --host=localhost --user=root --password=mysecretpassword --database=shop_db --table=orders --dry-run
```

### Example with Multiple Tables

You can align multiple tables by using a wildcard pattern. For example, to align all tables starting with `orders_`:

```bash
pt-align --host=localhost --user=root --password=mysecretpassword --database=shop_db --table='orders_*'
```

This command will optimize all tables in the `shop_db` database that match the pattern `orders_*`.

## How It Works

1. **Table Copy**: `pt-align` creates a temporary copy of the table.
2. **Re-insertion**: It re-inserts all rows into the new table, effectively reordering the storage.
3. **Table Drop & Rename**: The old table is dropped, and the new table is renamed.

This process helps to remove fragmentation and reorganize the table’s physical storage, optimizing query performance.

## Notes

- `pt-align` is primarily designed for InnoDB tables.
- Always create a backup before performing any operation that alters table structures.
- The command is ideal for large tables where fragmentation may significantly impact performance.

## Conclusion

`pt-align` is a powerful tool for improving table performance by fixing fragmentation in MySQL or MariaDB databases. It is a good practice to periodically align tables, especially in systems with heavy insertions and deletions.

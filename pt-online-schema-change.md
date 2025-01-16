# Percona Toolkit: pt-online-schema-change

`pt-online-schema-change` is a tool for performing non-blocking schema changes on MySQL tables. It works by creating a shadow table, copying data in chunks, and swapping the original table with the new one once the operation is complete, ensuring minimal impact on performance.

## Installation

### Debian/Ubuntu:
```bash
sudo apt-get install percona-toolkit
```

### RHEL/CentOS:
```bash
sudo yum install percona-toolkit
```

## Basic Usage

```bash
pt-online-schema-change --alter "ADD COLUMN new_column INT" --execute D=your_db,t=your_table
```

### Parameters:
- `--alter`: Specifies the DDL command (e.g., `ADD COLUMN`).
- `--execute`: Executes the change, use `--dry-run` to simulate.
- `--chunk-size`: Defines how many rows to copy at once.

## Advanced Features

### Archive Data:
```bash
pt-online-schema-change --alter "ADD COLUMN new_column INT" --execute D=your_db,t=your_table
```

### Delete Data:
To delete rows after archiving, use the `--purge` option:
```bash
pt-online-schema-change --alter "ADD COLUMN new_column INT" --execute D=your_db,t=your_table --purge
```

### Use Multiple Threads:
Use multiple threads to process data quickly:
```bash
pt-online-schema-change --alter "ADD COLUMN new_column INT" --execute D=your_db,t=your_table --threads 4
```

## Additional Options
- `--dry-run`: Simulate the change without making any modifications.
- `--progress`: Display progress information during the operation.
- `--no-lock`: Avoid locking the table during the operation.

## Conclusion

`pt-online-schema-change` is an essential tool for performing non-blocking schema changes on large MySQL or MariaDB tables. By offering features like chunking, multi-threading, and minimal table locking, it allows for efficient and safe schema modifications even in production environments.

For more detailed information, visit the official [Percona Documentation](https://docs.percona.com/percona-toolkit/pt-online-schema-change.html).

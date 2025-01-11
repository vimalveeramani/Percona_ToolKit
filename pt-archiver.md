
# Percona Toolkit: pt-archiver

`pt-archiver` is a tool for efficiently archiving or deleting rows from a MySQL or MariaDB table. It is designed to work on large tables with minimal impact on performance by using efficient techniques for archiving and purging data.

## Installation

Percona Toolkit is available in various package formats. You can download it from the official website or install it using your system's package manager.

### Installation on Debian/Ubuntu

```bash
sudo apt-get install percona-toolkit
```

### Installation on RHEL/CentOS

```bash
sudo yum install percona-toolkit
```

## Basic Usage

The basic syntax for using `pt-archiver` is:

```bash
pt-archiver --source h=localhost,D=test,t=big_table --where "id > 10000" --archive h=localhost,D=archive,t=big_table
```

### Parameters:

- `--source`: Specifies the source database and table (`h=host,D=database,t=table`).
- `--where`: A condition to filter the rows to be archived.
- `--archive`: Specifies the destination for the archived data.
  
This command copies rows matching the condition from the source table to the destination table.

## Features

### Archive Data

You can move data from one table to another, effectively archiving it:

```bash
pt-archiver --source h=localhost,D=test,t=big_table --where "id > 10000" --archive h=localhost,D=archive,t=big_table
```

### Delete Data

If you want to delete rows from the source table after archiving, use the `--purge` option:

```bash
pt-archiver --source h=localhost,D=test,t=big_table --where "id > 10000" --archive h=localhost,D=archive,t=big_table --purge
```

### Specify Chunk Size

To control the number of rows processed per batch, use the `--limit` option:

```bash
pt-archiver --source h=localhost,D=test,t=big_table --where "id > 10000" --archive h=localhost,D=archive,t=big_table --limit 1000
```

This will process up to 1000 rows at a time.

### Use Multiple Threads

You can use multiple threads to process data more quickly by specifying the `--no-check-charset` and `--threads` options:

```bash
pt-archiver --source h=localhost,D=test,t=big_table --where "id > 10000" --archive h=localhost,D=archive,t=big_table --threads 4
```

This will use 4 threads to process the data.

### Avoid Locking the Table

To minimize locking on the source table, you can use the `--no-lock` option:

```bash
pt-archiver --source h=localhost,D=test,t=big_table --where "id > 10000" --archive h=localhost,D=archive,t=big_table --no-lock
```

This avoids locking the table during the operation.

## Options

`pt-archiver` has many other options, such as:

- `--dry-run`: Perform a dry run without actually changing anything.
- `--progress`: Display progress information.
- `--no-check-charset`: Avoid checking for character set compatibility.
- `--lock-tables`: Lock the tables when archiving.

For a full list of options, see the official documentation:

[Percona Toolkit Documentation](https://docs.percona.com/percona-toolkit/)

## Conclusion

`pt-archiver` is an efficient tool for archiving or deleting large volumes of data from MySQL and MariaDB tables. By leveraging options like chunking, threading, and minimizing locking, it can help you perform these operations with minimal impact on your database performance.

For more information and advanced usage, refer to the [Percona Toolkit Documentation](https://docs.percona.com/percona-toolkit/).
```

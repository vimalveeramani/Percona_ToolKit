# pt-duplicate-key-checker

## Overview

`pt-duplicate-key-checker` is a Percona Toolkit utility for detecting duplicate and redundant indexes in MySQL databases. It helps optimize database performance by identifying unnecessary indexes that can be removed safely.

## Features
- Detects duplicate and redundant indexes.
- Works with MySQL and Percona Server.
- Provides recommendations for index optimization.
- Supports various filtering options.
- Can analyze multiple databases and tables.
- Offers suggestions for safe index removal.

## Installation

To install `pt-duplicate-key-checker`, you need to have Percona Toolkit installed. You can install it using the following commands:

```sh
# On Debian/Ubuntu
sudo apt update && sudo apt install percona-toolkit

# On RHEL/CentOS
sudo yum install percona-toolkit

# Using Homebrew on macOS
brew install percona-toolkit
```

## Syntax

```sh
pt-duplicate-key-checker [OPTIONS]
```

## Usage

Run the tool with the following basic command:

```sh
pt-duplicate-key-checker --host=localhost --user=root --password=yourpassword
```

### Example Output

If your database contains redundant indexes, the output will look something like this:

```sh
# Duplicate keys on test.table_name:
# PRIMARY KEY and KEY `id_idx` are duplicates. Both are defined on `id` column.
# DROP KEY `id_idx` on `test`.`table_name`;

# Duplicate keys on test.another_table:
# UNIQUE KEY `email_unique` and KEY `email_idx` are duplicates.
# DROP KEY `email_idx` on `test`.`another_table`;
```

## Options

- `--host=<host>`: Specify the database host.
- `--user=<user>`: Specify the database user.
- `--password=<password>`: Provide the database password.
- `--databases=<db1,db2,...>`: Limit the check to specific databases.
- `--tables=<table1,table2,...>`: Check only specific tables.
- `--ignore-databases=<db1,db2,...>`: Exclude specific databases from the check.
- `--ignore-tables=<table1,table2,...>`: Exclude specific tables.
- `--ask-pass`: Prompt for password securely.
- `--socket=<socket>`: Specify the MySQL socket file.
- `--port=<port>`: Specify the MySQL server port.

## Example with Multiple Databases

```sh
pt-duplicate-key-checker --host=127.0.0.1 --user=root --password=yourpassword --databases=mydb1,mydb2
```

## Best Practices
- Run this tool in a test environment before applying changes in production.
- Always take a backup before removing indexes.
- Review suggestions manually to avoid unintended performance issues.
- Consider impact on query performance before dropping indexes.

## More Information
For complete documentation, visit the [official Percona documentation](https://docs.percona.com/percona-toolkit/pt-duplicate-key-checker.html).



# Percona Toolkit: pt-find

`pt-find` is a command-line tool in Percona Toolkit that helps to find tables that match specific conditions within a MySQL database. It is useful for finding certain types of tables (e.g., those with a high number of rows, large disk usage, or specific table names). 

## Installation

Before using `pt-find`, ensure you have Percona Toolkit installed on your system. You can install it using the following methods:

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

For more installation methods, refer to the official [Percona Toolkit Installation Guide](https://www.percona.com/doc/percona-toolkit/).

## Usage

```bash
pt-find [OPTIONS] DSN
```

Where:
- `DSN` is the Data Source Name, which typically follows the format: `user:password@host/database`
- `OPTIONS` are the optional parameters to refine your query.

### Common Options
- `--where`: Specify conditions to filter results, such as filtering by table size or row count.
- `--tables`: Limit the query to specific tables.
- `--limit`: Restrict the number of rows returned.
- `--help`: Show help and usage details.

## Example Usage

### 1. Find Tables Larger than 1GB
This command searches for all tables in the `example_db` database on the localhost that are larger than 1GB in size.

```bash
pt-find --where 'data_length > 1073741824' --host=localhost --user=root --password=yourpassword example_db
```

### 2. Find Tables with More than 1 Million Rows
To find tables in `fl_db` with more than 1 million rows:

```bash
pt-find --where 'table_rows > 1000000' --host=localhost --user=root --password=yourpassword fl_db
```

### 3. Find Tables Matching Specific Name Pattern
To find all tables with names starting with `archive_`:

```bash
pt-find --where 'table_name LIKE "archive_%"' --host=localhost --user=root --password=yourpassword example_db
```

## Output

The tool will output the list of matching tables based on the conditions provided. Each line will show the database name, table name, and relevant metrics like row count and table size.

Example output:

```
example_db.archive_2020 1000000 2.5GB
example_db.archive_2021 1500000 3.2GB
```

## Conclusion

`pt-find` is a powerful tool to identify specific tables within a MySQL database that meet certain criteria. It can be used for various purposes like monitoring table sizes, row counts, or naming patterns. You can combine different conditions to focus on the most important aspects of your database.



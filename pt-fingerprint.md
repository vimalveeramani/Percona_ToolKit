
# pt-fingerprint - Convert Queries into Fingerprints

`pt-fingerprint` is part of the Percona Toolkit. It helps you convert SQL queries into abstracted, grouped fingerprints, allowing similar queries to be treated as one. This tool is useful for analyzing and optimizing query performance by normalizing query patterns.


## Installation

You can download the latest release of Percona Toolkit from the official site:

- [Percona Toolkit Download](http://www.percona.com/software/percona-toolkit/)
- Or, get the latest release directly via command line:

```bash
wget percona.com/get/percona-toolkit.tar.gz
wget percona.com/get/percona-toolkit.rpm
wget percona.com/get/percona-toolkit.deb
```

You can also get individual tools like `pt-fingerprint`:

```bash
wget percona.com/get/pt-fingerprint
```

## Usage

`pt-fingerprint` converts queries into fingerprints, either from the command line or from files.

### Convert a Single Query:
```bash
pt-fingerprint --query "SELECT a, b, c FROM users WHERE id = 500"
```

### Convert a File Full of Queries:
```bash
pt-fingerprint /path/to/file.txt
```

### Convert from Standard Input:
```bash
pt-fingerprint -
```

## Options

The tool accepts several options to customize its behavior:

- `--config`: Read a comma-separated list of config files (must be the first option).
- `--help`: Show help and exit.
- `--match-embedded-numbers`: Match numbers embedded in words (e.g., `catch22` will be replaced as a placeholder).
- `--match-md5-checksums`: Match MD5 checksums and replace them with a placeholder.
- `--query`: Specify the query to convert into a fingerprint.
- `--version`: Show version and exit.

## Example Usage

1. **Converting a Single Query:**

```bash
pt-fingerprint --query "SELECT name, password FROM user WHERE id='12823';"
```

The output would be the fingerprint for the query:
```
select name, password from user where id=?
```

2. **Converting a File of Queries:**

```bash
pt-fingerprint /path/to/queries.txt
```

The tool will read each query from the file and generate fingerprints for them.

## Risks

- `pt-fingerprint` is a mature, well-tested tool but should be used with caution.
- Always read the tool’s documentation, review known bugs, and test it on a non-production server.
- Backup your production server and verify the backups before using this tool in a production environment.

## System Requirements

- Perl
- DBI
- DBD::mysql
- Required core Perl packages, which are typically included in most modern Perl versions.

## Environment

To enable debugging and capture all output, use the `PTDEBUG` environment variable:

```bash
PTDEBUG=1 pt-fingerprint ... > FILE 2>&1
```

Be cautious when using debug mode, as it may expose sensitive information (e.g., passwords).



## License

This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License version 2 or the Perl Artistic License.

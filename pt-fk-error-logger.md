
# pt-fk-error-logger - Log MySQL Foreign Key Errors

## Overview
`pt-fk-error-logger` is a tool from Percona Toolkit designed to log MySQL foreign key errors. It logs information from the `SHOW ENGINE INNODB STATUS` output and can save it to a table. The tool continuously monitors for new foreign key errors, providing detailed logging for database administrators.

## Features
- Continuously monitors for new foreign key errors.
- Prints or saves foreign key error information from `SHOW ENGINE INNODB STATUS`.
- Can be set to run for a specified amount of time or iterations.
- Errors can be stored in a database table for further analysis.

## Installation

Download the latest release of Percona Toolkit or the individual tools using the following commands:

```bash
wget percona.com/get/percona-toolkit.tar.gz
wget percona.com/get/percona-toolkit.rpm
wget percona.com/get/percona-toolkit.deb
```

To get the latest release of the `pt-fk-error-logger` tool:

```bash
wget percona.com/get/pt-fk-error-logger
```

## Usage

### Print foreign key errors

To log foreign key errors on a MySQL host:

```bash
pt-fk-error-logger h=host1
```

### Print foreign key errors once then exit

To print foreign key errors once and then exit:

```bash
pt-fk-error-logger h=host1 --iterations 1
```

### Save foreign key errors to a table

To save foreign key errors on one host and store them in a table on another:

```bash
pt-fk-error-logger h=host1 --dest h=host2,D=percona_schema,t=fke
```

## Options

| Option              | Description                                                                                                                                   |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `--ask-pass`         | Prompt for a password when connecting to MySQL.                                                                                               |
| `--charset`          | Default character set. If set to `utf8`, enables UTF-8 support for MySQL connections.                                                         |
| `--config`           | Read this comma-separated list of config files.                                                                                                |
| `--daemonize`        | Fork the process to the background (POSIX systems only).                                                                                      |
| `--database`         | Connect to this database.                                                                                                                     |
| `--defaults-file`    | Only read MySQL options from the given file (must be an absolute pathname).                                                                   |
| `--dest`             | DSN to save foreign key errors to a table. Must specify the database and table.                                                                |
| `--host`             | Connect to the specified host.                                                                                                                |
| `--interval`         | Interval in seconds to check for foreign key errors (default: 30).                                                                             |
| `--iterations`       | The number of iterations to run before exiting.                                                                                               |
| `--log`              | Print all output to the specified file when daemonized.                                                                                        |
| `--password`         | Password for MySQL connection.                                                                                                                |
| `--pid`              | Create the given PID file.                                                                                                                   |
| `--quiet`            | Do not print foreign key errors, only print warnings and errors.                                                                              |
| `--run-time`         | Duration to run before exiting.                                                                                                               |
| `--user`             | MySQL user for login.                                                                                                                         |
| `--version`          | Show the version and exit.                                                                                                                   |

## Example: Save Errors to Table

```bash
pt-fk-error-logger h=host1 --dest h=host2,D=percona_schema,t=fke
```

This saves foreign key errors on `host1` to the `fke` table in the `percona_schema` database on `host2`.

## Requirements

- Perl
- DBI, DBD::mysql modules
- MySQL server running with InnoDB engine

## Risks

Percona Toolkit tools, including `pt-fk-error-logger`, are mature and well-tested, but you should take precautions before using them in a production environment:

- Test the tool on a non-production server.
- Backup your production server and verify the backups.

## Bug Reporting

If you encounter issues or bugs, please report them to [Percona JIRA](https://jira.percona.com/projects/PT/issues). Include the following:

- The command-line used to run the tool.
- Tool version.
- MySQL version of all servers involved.
- Output from the tool (including STDERR).
- Input files (log/dump/config files).

## Authors

- Daniel Nichter

## License

This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License or the Perl Artistic License.

## Version

`pt-fk-error-logger` 3.7.0
```

This README provides a structured overview, usage examples, options, and other key information needed to use the `pt-fk-error-logger` tool.

# pt-config-diff

## Overview
`pt-config-diff` is a tool from [Percona Toolkit](https://www.percona.com/software/database-tools/percona-toolkit) designed to compare MySQL configuration files. It highlights differences in system variables between different MySQL instances or configuration files, making it useful for database administrators managing multiple servers.

## Features
- Compares MySQL configuration files or running instances.
- Identifies differences in system variables.
- Supports JSON and other structured output formats.
- Works with remote MySQL servers.

## Installation
Ensure you have Percona Toolkit installed. If not, install it using:
```sh
sudo apt-get install percona-toolkit  # Debian/Ubuntu
yum install percona-toolkit            # RHEL/CentOS
brew install percona-toolkit            # macOS
```

## Usage
### Basic Comparison
Compare two MySQL configuration files:
```sh
pt-config-diff /etc/mysql/my.cnf /backup/my-old.cnf
```

### Comparing Running MySQL Instances
```sh
pt-config-diff h=localhost,u=root,p=secret h=remotehost,u=root,p=secret
```

### JSON Output Format
```sh
pt-config-diff --format=json h=localhost,u=root,p=secret h=remotehost,u=root,p=secret
```

## Example Output
```
Differences:
  variable_name_1:  value1  !=  value2
  variable_name_2:  value3  !=  value4
```

## Use Cases
- Validate configuration consistency across MySQL servers.
- Detect unintended changes in configuration files.
- Audit MySQL settings before and after migrations.

## Documentation
For more details, visit the [official documentation](https://docs.percona.com/percona-toolkit/pt-config-diff.html).

## License
Percona Toolkit is released under the [GNU General Public License (GPL), Version 2](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

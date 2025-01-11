# pt-align - Aligning Output for Better Readability

## Overview

**pt-align** is a command-line utility from Percona Toolkit that helps align text-based output into properly formatted columns. It is particularly useful for improving the readability of outputs from system monitoring tools like `vmstat` and `iostat`.

## Usage

```bash
pt-align [FILES]
```

If no files are specified, `pt-align` reads from standard input (STDIN). It takes input with misaligned columns and adjusts the spacing to make it easier to read. 

### Example

#### Input:
```
DATABASE TABLE   ROWS
foo      bar      100
long_db_name table  1
another  long_name 500
```

#### Output:
```
DATABASE     TABLE     ROWS
foo          bar        100
long_db_name table        1
another      long_name  500
```

## Key Features

- Automatically detects column widths and aligns data accordingly.
- Useful for improving readability of structured text output.
- Works with various command outputs, including database query results and system monitoring tools.

## Risks and Precautions

While `pt-align` itself is a non-intrusive tool, all Percona Toolkit utilities should be used with care. Before using:

- Read the official documentation.
- Check for any known issues or bugs.
- Test the tool on a non-production environment.
- Ensure you have backups if working with sensitive data.

## How It Works

1. Reads input line by line and splits each line into words.
2. Determines the predominant number of words per line.
3. Identifies header and data lines based on format consistency.
4. Determines whether words are numeric or text for proper column alignment.
5. Adjusts column widths and prints the formatted output.

## Available Options

- `--help` : Displays help information and exits.
- `--version` : Displays the current version and exits.

## System Requirements

- Requires **Perl** and core Perl modules, which are typically available in standard installations.

## Reporting Issues

To report bugs, visit [Percona JIRA](https://jira.percona.com/projects/PT). When reporting issues, include:

- The exact command used
- The version of `pt-align`
- The MySQL version, if applicable
- Any relevant input/output examples
- Debug output if possible (`PTDEBUG` mode)

**Caution:** `PTDEBUG` may expose sensitive command-line parameters, including passwords.

## Installation and Download

Download the latest release from [Percona Toolkit](http://www.percona.com/software/percona-toolkit/):

```bash
wget percona.com/get/percona-toolkit.tar.gz
wget percona.com/get/percona-toolkit.rpm
wget percona.com/get/percona-toolkit.deb
```

To download individual tools:
```bash
wget percona.com/get/TOOL  # Replace TOOL with the specific tool name
```

## Contributors

- **Baron Schwartz**
- **Brian Fraser**
- **Daniel Nichter**

## About Percona Toolkit

Percona Toolkit is a collection of advanced command-line tools for MySQL database management, developed by Percona. The toolkit originated from two projects, **Maatkit** and **Aspersa**, which were merged in 2011.

For more tools, visit [Percona Software](http://www.percona.com/software/).

## License and Warranty

This software is licensed under:
- **GNU General Public License (GPL v2)**
- **Perl Artistic License**

For license details, use:
```bash
man perlgpl
man perlartistic
```

If you did not receive a copy of the GNU General Public License, write to:
```
Free Software Foundation, Inc.
59 Temple Place, Suite 330
Boston, MA 02111-1307 USA
```

## Version

Current version: **pt-align 3.7.0**


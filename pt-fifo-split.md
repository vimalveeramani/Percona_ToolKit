
# pt-fifo-split: Percona Toolkit

`pt-fifo-split` is a tool from Percona Toolkit that helps split a large file into multiple smaller files and process them in parallel. This is useful when dealing with very large data sets or logs, allowing you to divide the task into smaller, manageable chunks.



## Installation

You can install Percona Toolkit on a Linux system using `apt` (Debian/Ubuntu) or `yum` (CentOS/RedHat) package managers.

For Debian/Ubuntu:
```bash
sudo apt-get install percona-toolkit
```

For CentOS/RedHat:
```bash
sudo yum install percona-toolkit
```

Alternatively, you can download and install the toolkit from the official Percona website:  
[Percona Toolkit Download](https://www.percona.com/downloads/percona-toolkit/)

## Usage

`pt-fifo-split` helps you split a large file into smaller, more manageable parts and allows you to run processes on those files in parallel. Below is the basic syntax:

```bash
pt-fifo-split --file <input-file> --split-size <size-in-bytes> -- <command>
```

- `--file <input-file>`: Path to the input file that will be split.
- `--split-size <size-in-bytes>`: Size of each split file in bytes.
- `<command>`: Command to run on each split file.

## Options

- `--file`  
  The input file to be split.
  
- `--split-size`  
  The size (in bytes) for each split file.
  
- `--parallel`  
  Number of parallel processes to run. Default is 1.

- `--output`  
  Output directory for the split files.

For a full list of options, run the following command:

```bash
pt-fifo-split --help
```

## Example

Suppose you have a large log file, `large_file.txt`, and want to split it into smaller chunks of 10MB each to process in parallel. Here’s how you can do it:

1. Split `large_file.txt` into smaller 10MB chunks and process each chunk with the `cat` command (you can replace `cat` with any other processing command).

```bash
pt-fifo-split --file large_file.txt --split-size 10485760 --parallel 4 -- cat
```

This command will:
- Split `large_file.txt` into chunks of 10MB each.
- Process the chunks in parallel using 4 processes.
- Each chunk will be passed to the `cat` command (or replace `cat` with any other command for your use case).

## License

This tool is part of Percona Toolkit, which is released under the **GPL 2.0** license.

For more information, please refer to the official [Percona Toolkit Documentation](https://docs.percona.com/percona-toolkit/).
```


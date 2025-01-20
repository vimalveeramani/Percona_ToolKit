
`pt-galera-log-explainer` is part of the **Percona Toolkit**. You can install it on Linux, macOS, or from the source.

#### **Install on Linux (Ubuntu/Debian)**

1. **Add Percona repository**:
   ```bash
   wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb
   sudo dpkg -i percona-release_latest.generic_all.deb
   sudo apt-get update
   ```

2. **Install Percona Toolkit**:
   ```bash
   sudo apt-get install percona-toolkit
   ```

#### **Install on Linux (CentOS/RHEL)**

1. **Add Percona repository**:
   ```bash
   sudo yum install https://repo.percona.com/yum/percona-release-1.0-22.noarch.rpm
   ```

2. **Install Percona Toolkit**:
   ```bash
   sudo yum install percona-toolkit
   ```

#### **Install on macOS (Using Homebrew)**

1. **Install Homebrew** (if you don’t have it yet):
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **Install Percona Toolkit**:
   ```bash
   brew install percona-toolkit
   ```

#### **Install from Source (If needed)**

1. **Download the latest version** of Percona Toolkit from [GitHub](https://github.com/percona/percona-toolkit) or [Percona](https://www.percona.com/software/percona-toolkit).

2. **Extract the tarball**:
   ```bash
   tar -xvzf percona-toolkit-*.tar.gz
   ```

3. **Navigate to the directory** and install:
   ```bash
   cd percona-toolkit-*
   sudo make install
   ```

---

### **2. Verify the Installation**

Once installed, verify that the `pt-galera-log-explainer` command is available:

```bash
pt-galera-log-explainer --version
```

This should display the version of Percona Toolkit.

---

### **3. Using `pt-galera-log-explainer` to Analyze Galera Logs**

Now that Percona Toolkit is installed, you can use `pt-galera-log-explainer` to filter, aggregate, and summarize Galera logs.

#### **List Key Events in Galera Logs**
Use the `list` command to list events such as SST, view changes, errors, and more.

Example: List all events from logs in `/var/log/mysql/*.log` from a specific date range:
```bash
pt-galera-log-explainer list --all --since 2023-01-05T03:24:26.000000Z --until 2023-01-05T03:44:59.855491Z /var/log/mysql/*.log
```

You can also filter by specific event types, such as:
- `--sst` (for SST events)
- `--views` (for view changes)
- `--events` (for general events)

Example: List only SST and view change events:
```bash
pt-galera-log-explainer list --sst --views *.log
```

#### **Find Information about Nodes Using `whois`**

You can find information about a node using its IP, UUID, or node name. Example:

```bash
pt-galera-log-explainer whois '172.17.0.2' --no-color mysql.log
```

This will display detailed information such as:
- Node names
- UUID mappings
- Log timestamps for the specific node

#### **List Replication Failures (Conflicts)**

To list replication failures (Galera 4 conflicts), use the `conflicts` command:

```bash
pt-galera-log-explainer conflicts --json *.log
```

This will output the conflicts in JSON format. You can also use `--yaml` for YAML output.

#### **Get Context for a Log File (`ctx`)**

To get detailed information about a specific log file, including version, SST info, UUID-IP mappings, etc., use the `ctx` command:

```bash
pt-galera-log-explainer ctx mysql.log
```

#### **View Implemented Regexes (`regex-list`)**

If you want to see the regex patterns used by the tool, you can list them:

```bash
pt-galera-log-explainer regex-list
```

---

### **Additional Flags and Options**

- **`--no-color`**: Removes color from output.
- **`--since` / `--until`**: Filters logs to events between the specified dates (RFC3339 format).
- **`--merge-by-directory`**: Merges logs by their base directory for better organization.
- **`--pxc-operator`**: Fine-tunes the regexes for Percona PXC operator logs.
- **`--skip-merge`**: Disables merging of logs together.
- **`-v`, `-vv`**: Set verbosity levels for more detailed output.

---

### **Example Outputs**

**List key events:**
```bash
pt-galera-log-explainer list --all --no-color --since=2023-03-12T19:41:28.493046Z --until=2023-03-12T19:44:59.855491Z tests/logs/upgrade/*
```
Output example:
```
2023-03-12T19:41:28.493046Z   starting(8.0.28)                           |                                       |
2023-03-12T19:43:17.630191Z   |                                          node3 joined                            |
2023-03-12T19:43:18.130916Z   OPEN -> PRIMARY                            |                                       |
2023-03-12T19:43:18.904410Z   will receive IST(seqno:178226792)          |                                       |
2023-03-12T19:44:58.999603Z   |                                          |                                       node1 cannot find donor
```

**Node info with `whois`:**
```bash
pt-galera-log-explainer whois 172.17.0.2 --no-color tests/logs/upgrade/*
```
Output example:
```
ip:
└── 172.17.0.2
    ├── nodename:
    │   └── node1 (2023-03-12 19:35:07.644683 +0000 UTC)
    │
    └── uuid:
        ├── 1d3ea8f5 (2023-03-12 07:24:13.789261 +0000 UTC)
        ├── 54ab931e (2023-03-12 07:43:08.563339 +0000 UTC)
```

---

### **Requirements**

- **grep (version 3)**: If you’re on macOS, `grep` may need to be set to `ggrep` due to licensing restrictions.
- **Compatible with Percona XtraDB Cluster (5.5 to 8.0)** and **MariaDB Galera Cluster (10.0 to 10.6)**.

---

### **Known Issues**

- Nodes with the same IP or identical names may not be supported.
- Sparse file identification might be missed; use `--merge-by-directory` if your logs are organized by node.
- Column widths for SST events may be too large for easy readability.

---

With these steps, you should be able to install and effectively use `pt-galera-log-explainer` to troubleshoot and analyze your Galera Cluster logs!

The Linux file system is a hierarchical structure that organizes data in a tree-like format. At the top of this structure is the **root directory**, represented by a single forward slash (`/`). Everything on a Linux system is located under this root directory.

Here's a breakdown of the main directories you'll typically find in a Linux file system:

---

### 🌳 **Top-Level Directory Structure (Root `/`)**

| Directory | Purpose                                                                                             |
| --------- | --------------------------------------------------------------------------------------------------- |
| `/`       | The root directory. All files and directories start from here.                                      |
| `/bin`    | Essential **binary** executables used during booting and single-user mode (e.g., `ls`, `cp`, `mv`). |
| `/boot`   | Contains the boot loader files, including the Linux kernel.                                         |
| `/dev`    | Contains **device files** for hardware (e.g., `/dev/sda`, `/dev/null`).                             |
| `/etc`    | System-wide **configuration files** (e.g., network config, user accounts).                          |
| `/home`   | Home directories for users (e.g., `/home/alice`).                                                   |
| `/lib`    | Essential **shared libraries** for binaries in `/bin` and `/sbin`.                                  |
| `/media`  | Mount points for **removable media** (e.g., USB drives, CDs).                                       |
| `/mnt`    | Temporary mount point for **manual mounting** of filesystems.                                       |
| `/opt`    | Optional **third-party software packages**.                                                         |
| `/proc`   | A **virtual filesystem** exposing kernel and process information.                                   |
| `/root`   | Home directory for the **root** user.                                                               |
| `/run`    | Holds runtime data for processes since boot.                                                        |
| `/sbin`   | System **binaries** used for system administration (e.g., `fsck`, `reboot`).                        |
| `/srv`    | Contains **service data** (e.g., files for web or FTP servers).                                     |
| `/sys`    | Interface to **kernel devices**, similar to `/proc`.                                                |
| `/tmp`    | Temporary files. Can be cleared on reboot.                                                          |
| `/usr`    | Secondary hierarchy for **user programs**, libraries, docs (`/usr/bin`, `/usr/lib`).                |
| `/var`    | Variable data like **logs**, mail, spool files, and databases.                                      |

---

### 📂 Example Hierarchy

```
/
├── bin/
├── boot/
├── dev/
├── etc/
│   ├── passwd
│   └── network/
├── home/
│   └── alice/
├── lib/
├── media/
├── mnt/
├── opt/
├── proc/
├── root/
├── run/
├── sbin/
├── srv/
├── sys/
├── tmp/
├── usr/
│   ├── bin/
│   └── lib/
└── var/
```

---

### Key Concepts

* **Everything is a file**: Devices, directories, and even processes are represented as files.
* **Mounting**: External filesystems (e.g., USB, network shares) are **mounted** into the hierarchy rather than assigned drive letters.
* **Permissions**: Access control is enforced using **user/group/other** and **read/write/execute** permissions.

---


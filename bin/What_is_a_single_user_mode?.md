## What is a single user mode?

**Single-user mode** in Linux (also called **rescue mode** or **maintenance mode**) is a special **runlevel** or boot mode where the system starts **with minimal services and only one user: the superuser (root)**.

---

### 🧭 Purpose of Single-User Mode

It's used mainly for **system maintenance** or **emergency troubleshooting**, such as:

* Fixing corrupted filesystems
* Resetting forgotten root passwords
* Repairing misconfigured system files (e.g., `/etc/fstab`)
* Troubleshooting boot issues
* Removing stuck locks or processes
* Recovering from hardware failures

---

### ⚙️ What Happens in Single-User Mode

* No graphical interface (no GUI)
* No network services (e.g., no SSH, internet)
* Only **root** has access
* Only **essential file systems** are mounted (often read-only)
* Minimal background processes or daemons are running

It's essentially a **safe mode** with **full root privileges** but **no multi-user or network activity** — which makes it perfect for critical repairs.

---

### 🏁 How to Enter Single-User Mode

You can enter it during system boot in different ways depending on your bootloader:

#### For GRUB-based systems:

1. Reboot your system.
2. At the GRUB menu, highlight your Linux kernel and press `e` to edit.
3. Find the line starting with `linux` or `linux16`.
4. Add `single` or `init=/bin/bash` at the end of that line.
5. Press `Ctrl + X` or `F10` to boot.

✅ You’ll boot into single-user mode with root access.

> For newer systems using `systemd`, you can also use `systemd.unit=rescue.target` or `emergency.target` instead of `single`.

---

### 🚨 Security Note

Single-user mode gives **full control** of the system **without needing a password** on many distributions (unless explicitly protected). So physical access = root access unless you **secure GRUB with a password**.

---

### 🔄 Exit Single-User Mode

When you’re done:

* Type `reboot` or `exec /sbin/init` (or `systemctl default`) to go back to multi-user mode.
* Ensure any changes are saved, especially if the root filesystem was mounted as read-only.

---



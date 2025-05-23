## Examples  involving  USB  devices

Let’s explore more **advanced `/dev` usage** involving:

1. 🔌 **Detecting and working with USB devices**
2. 🧑‍💻 **Writing a simple custom character device driver (kernel module)**
3. ⚙️ **Automating device detection using `udev` rules**

---

## 🔌 1. **Working with USB Devices via `/dev`**

When you plug in a USB device (flash drive, camera, etc.), Linux creates a device file for it — typically under `/dev/sdX` (for storage) or `/dev/bus/usb` (for raw USB).

### 🧪 Example: Mount a USB drive manually

```bash
lsblk     # Find your USB device, e.g., /dev/sdb1
sudo mount /dev/sdb1 /mnt
```

### 🔍 Example: Monitor device events in real-time

```bash
udevadm monitor
```

This shows kernel and udev events when devices are added/removed.

---

## 🧑‍💻 2. **Simple Custom Character Device Driver (Kernel Module)**

This is a low-level example for educational use.

### 🧱 Step 1: A minimal kernel module

**`simple_char.c`**

```c
#include <linux/init.h>
#include <linux/module.h>
#include <linux/fs.h>

#define DEVICE_NAME "simple_char"
static int major;

static int dev_open(struct inode *, struct file *) { return 0; }
static int dev_release(struct inode *, struct file *) { return 0; }
static struct file_operations fops = {
    .open = dev_open,
    .release = dev_release,
};

static int __init simple_char_init(void) {
    major = register_chrdev(0, DEVICE_NAME, &fops);
    if (major < 0) {
        printk(KERN_ALERT "Failed to register a major number\n");
        return major;
    }
    printk(KERN_INFO "Registered simple_char with major %d\n", major);
    return 0;
}

static void __exit simple_char_exit(void) {
    unregister_chrdev(major, DEVICE_NAME);
    printk(KERN_INFO "Unregistered simple_char\n");
}

module_init(simple_char_init);
module_exit(simple_char_exit);
MODULE_LICENSE("GPL");
```

### ⚙️ Step 2: Compile and load

```bash
make -C /lib/modules/$(uname -r)/build M=$PWD modules
sudo insmod simple_char.ko
```

### 🔌 Step 3: Create device file and test

```bash
sudo mknod /dev/simple_char c <major_number> 0
sudo chmod 666 /dev/simple_char
```

Replace `<major_number>` with the one shown in `dmesg`.

---

## ⚙️ 3. **Automate with `udev` Rules**

`udev` allows you to trigger actions when devices appear/disappear.

### 🧩 Example: Auto-mount USB drive or set permissions

**Step 1: Identify attributes**

```bash
udevadm info --query=all --name=/dev/sdb1
```

**Step 2: Create a rule**

```bash
sudo nano /etc/udev/rules.d/99-usb-autoperm.rules
```

```udev
KERNEL=="sdb1", SUBSYSTEM=="block", ACTION=="add", MODE="0666"
```

**Step 3: Reload `udev`**

```bash
sudo udevadm control --reload-rules
```

Now, whenever `/dev/sdb1` appears, its permissions will be automatically set.

---

### ✅ Summary of What You Can Do

| Task                         | Tool/Method                |
| ---------------------------- | -------------------------- |
| Detect USB devices           | `udevadm monitor`, `lsblk` |
| Write custom char device     | Kernel module + `/dev/`    |
| Automate device handling     | `udev` rules               |
| Create device files manually | `mknod`                    |

---



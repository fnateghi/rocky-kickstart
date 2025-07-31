# Rocky Linux Kickstart Installer

Automate the installation of **Rocky Linux 8 and 9** using a custom Kickstart file.  
This method works by manually editing the boot options when starting from the official Rocky Linux ISO.

---

## Overview

This repository contains Kickstart configuration files (`.cfg`) for automated installation of Rocky Linux with your preferred setup (e.g., users, packages, disk layout, Python version, etc.).

---

## must have 

To work correctly, the Kickstart file must be accessible over the network during installation. 
in my example i use apache html site where i placed the raw file.
You can host it using any network-accessible method, such as:

- A local or remote HTTP server
- A public Git repository with a raw file URL
- A TFTP, FTP, or NFS server

Make sure the target machine has network access and can reach the server hosting the Kickstart file.

---
## How to Use

### Step-by-Step Instructions

1. **Boot from the Rocky Linux ISO** (8 or 9).
2. When the **GRUB menu** appears, highlight `Install Rocky Linux` (but **do not press Enter**).
3. Press **`e`** to edit the boot parameters.
4. Find the line starting with:

    ```bash
    linux /images/pxeboot/vmlinuz inst.stage2=hd:LABEL=Rocky-9-3-x86_64-dvd quiet
    ```

5. Append your Kickstart file URL to the end of the line:

    ```bash
    inst.ks=http://<your-ip>/kickstart_rocky9.cfg
    ```

6. Boot with **Ctrl+X** or **F10** to start the automated installation.

---

## Example

```bash
linux /images/pxeboot/vmlinuz inst.stage2=hd:LABEL=Rocky-9-3-x86_64-dvd quiet inst.ks=http://192.168.1.1/kickstart_rocky9.cfg

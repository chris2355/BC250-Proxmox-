# Asrock BC-250 to Desktop Computer Conversion & Proxmox Cluster Setup

## Project Overview

This project focuses on transforming the Asrock BC-250 crypto miner into a functional desktop computer running the latest version of Ubuntu. Once Ubuntu is successfully installed, the goal is to set up Proxmox and create a cluster with multiple BC-250 units. This will involve several stages, including modifying BIOS settings, resolving compatibility issues with Ubuntu, and eventually setting up Proxmox for virtualized environments.

## Progress So Far

### 1. BIOS Modification for RAM Allocation
The first task was to modify the BIOS of the Asrock BC-250 to allow for manual control of RAM allocation between the CPU and GPU. By default, the system had a 50/50 split of 16GB of RAM, but after modifications, we now have full control over how much memory is allocated to each component.

This BIOS modification was made possible thanks to the invaluable work of [TuxThePenguin0](https://github.com/TuxThePenguin0) and [mothenjoyer69](https://github.com/mothenjoyer69/bc250-documentation), whose documentation provided the necessary groundwork for this project.

### 2. Ubuntu Installation

One of the next hurdles was getting Ubuntu to work on the BC-250. The latest versions of Ubuntu (6.5 kernel and beyond) have compatibility issues with the BC-250, causing display problems. The instructions in the repository of [mothenjoyer69](https://github.com/mothenjoyer69/bc250-documentation) provided a workaround for Fedora builds, but the solution was not directly applicable to Debian-based distributions like Ubuntu.

Here’s the fix that worked for installing Ubuntu:

#### Steps to Install Ubuntu:
1. **Use a Kernel Version Older Than 6.5:**
   - When creating the installation media, select a kernel version earlier than 6.5.
   - Boot into Ubuntu's installation in **Safe Graphics Mode**.

2. **Installation Process:**
   - Proceed with the installation as usual, selecting your desired partitions and options.

3. **Post-installation Steps:**
   - After the installation, during the reboot process, **tap the Shift key** to access the GRUB boot menu.
   - From the GRUB menu, select **Advanced Options** and choose to boot into **Recovery Mode**.

4. **Modify GRUB Configuration:**
   - Once in recovery mode, open the **root console**.
   - Edit the GRUB configuration file by running the following command:
     ```bash
     nano /etc/default/grub
     ```
   - Modify the line:
     ```bash
     GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
     ```
     To:
     ```bash
     GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nomodeset"
     ```

5. **Update GRUB Configuration:**
   - Run the following command to apply the changes:
     ```bash
     grub-mkconfig -o /boot/efi/EFI/ubuntu/grub.cfg
     ```

6. **Reboot the System:**
   - After making these changes, type `reboot` to restart the system. Ubuntu should now load without issues and be fully updatable.


# Proxmox Installation Instructions

The process for setting up Proxmox is similar to setting up Ubuntu, but with some key differences. Follow these steps carefully to ensure a smooth installation.

## Step 1: Download and Prepare Installation Media

1. Download the latest Proxmox release from the [official Proxmox website](https://www.proxmox.com/en/proxmox-ve).
2. Create a bootable USB drive with the Proxmox installer. You can use tools like **Rufus** for this process.
   - In Rufus, select the Proxmox ISO, choose the appropriate USB drive, and click "Start" to create the bootable media.

## Step 2: Install Proxmox

1. Insert the bootable USB into the BC-250 and power it on.
2. When the Proxmox installation screen appears, **highlight** the "Graphical Install" option but **don’t click** on it yet.
3. Press the **‘e’ key** to enter the GRUB bootloader options.
4. Find the line starting with `linux` and add `nomodeset` at the end of the line. This ensures proper display output during installation.
   - Example: 
     ```
     linux /install.amd/vmlinuz nomodeset
     ```
5. Press **F10** or **Ctrl+X** to continue the installation with the modified boot parameters.
6. Proceed with the Proxmox installation as you would with any standard Linux installation.

## Step 3: Post-Installation Configuration

After the installation completes, follow these steps to finalize the setup:

1. **Reboot the System:**
   - After the installation, during the reboot process, repeatedly tap the **Shift** key to access the GRUB boot menu.
2. **Access Recovery Mode:**
   - From the GRUB menu, select **Advanced Options** and then choose **Recovery Mode** to boot into a special environment for making changes.
3. **Modify GRUB Configuration:**
   - Once in recovery mode, open the root console.
   - Edit the GRUB configuration file by running:
     ```bash
     nano /etc/default/grub
     ```
   - Find the line starting with `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"`.
   - Modify it to include `nomodeset` at the end:
     ```bash
     GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nomodeset"
     ```
4. **Update GRUB:**
   - After saving the changes, update the GRUB configuration to apply the changes:
     ```bash
     grub-mkconfig -o /boot/efi/EFI/proxmox/grub.cfg
     ```

5. **Reboot the System:**
   - After updating GRUB, reboot the system:
     ```bash
     reboot
     ```

Now, Proxmox should boot correctly, and the system should display properly without graphical issues.

# Future Plans
 
1. **Cluster Setup:**
   - Set up a Proxmox cluster with multiple BC-250 units to create a high-performance, virtualized environment.

2. **Performance Testing:**
   - Once the cluster is established, conduct performance testing to ensure the BC-250 can handle the virtual machines and workloads expected from the setup.

---

## Contributions

Contributions are welcome! If you have any improvements or fixes, please fork the repository, make your changes, and submit a pull request. Be sure to follow the steps for proper installation and configuration.

---

## Acknowledgments

This project would not have been possible without the contributions of the following people and repositories:
- [TuxThePenguin0](https://github.com/TuxThePenguin0) for the initial work on modifying the BC-250 BIOS.
- [mothenjoyer69](https://github.com/mothenjoyer69/bc250-documentation) for providing the essential documentation and fixes related to the Ubuntu installation process.

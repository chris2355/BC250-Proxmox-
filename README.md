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

### 3. Next Steps: Proxmox Setup

The next milestone for this project is installing and configuring Proxmox on the BC-250. Once Ubuntu is running stably, the goal is to install Proxmox and create a Proxmox cluster with multiple BC-250 units to run virtual machines and containers.

---

## Future Plans

1. **Proxmox Installation:**
   - Install Proxmox on BC-250 and ensure that it integrates seamlessly with the system.

2. **Cluster Setup:**
   - Set up a Proxmox cluster with multiple BC-250 units to create a high-performance, virtualized environment.

3. **Performance Testing:**
   - Once the cluster is established, conduct performance testing to ensure the BC-250 can handle the virtual machines and workloads expected from the setup.

---

## Contributions

Contributions are welcome! If you have any improvements or fixes, please fork the repository, make your changes, and submit a pull request. Be sure to follow the steps for proper installation and configuration.

---

## Acknowledgments

This project would not have been possible without the contributions of the following people and repositories:
- [TuxThePenguin0](https://github.com/TuxThePenguin0) for the initial work on modifying the BC-250 BIOS.
- [mothenjoyer69](https://github.com/mothenjoyer69/bc250-documentation) for providing the essential documentation and fixes related to the Ubuntu installation process.

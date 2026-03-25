# homelab-setup
Guide to creating a Cybersecurity-focused homelab with virtual machines.

# Prerequisites
This guide follows my personal setup, which consists of the following:
* Workstation running Arch Linux
* 32GB RAM
* 12-Thread CPU

Additionally, below is a general list of what is required, which will be explained in detail later.
* Hypervisor
  * KVM
  * virt-manager
  * QEMU
  * Libvirt
* ISO files
  * OPNsense
  * Desktop OS (Linux or Windows)
  * Server OS (Linux or Windows)
  * Kali Linux

## Hypervisor Setup
Initially, let's focus on installing a hypervisor and other tools to help us create and manage virtual machines.

### KVM (Kernel-based Virtual Machine)
https://linux-kvm.org/page/Main_Page

### virt-manager (Virtual Machine Manager)
https://virt-manager.org/



# Creating Virtual Networks
For our purposes, the virtual network configuration requires two networks:
* A **WAN** link to connect the firewall to the Internet.
* A **LAN** link to connect the firewall to local endpoints (desktops, servers, etc.).

For now, it will suffice to use the NAT virtual network created by default in virt-manager for the WAN link.

To create the LAN virtual network in virt-manager:
1. Select, but do not open, the OPNsense VM that has been created.
2. Under the **Edit** tab, select **Connection Details**.
3. Navigate to the **Virtual Networks** tab, and select **Add Networks** at the bottom-left of the page.
4. In the **Create Virtual Networks** window:
   1. Change **Mode:** to **Isolated**
   2. Change **Name:** to LAN, Isolated, or something else that reminds you of its purpose.
   3. **IPv4 configuration**
      1. Disable DHCPv4 (Uncheck the **Enable DHCPv4** box). OPNsense will handle DHCP configuration.

# OPNsense
https://opnsense.org/

OPNsense is an open source firewall and routing platform.

## OPNsense Installation
1. Acquire the **dvd** image from OPNsense's website
2. Create a new virtual machine using the ISO file acquired.
   * OPNsense is based on FreeBSD
   * Minimum of 2 CPU threads
   * Minimum required RAM is 3 GB
   * Minimum virtual disk size is 8 GB
3. Review the configuration prior to installation
   * Add the NAT (WAN) and Isolated (LAN) networks to the VM
   * Make a note of the MAC addresses of each network.
4. Boot the virtual machine and begin installation
   1. Log in with the user **installer** and password **opnsense**
   2. Follow the installation process (filesystem, partitioning, disk selection, etc.)
   3. Set a root password
   4. Complete the installation

## OPNsense Initial Configuration
Log in using username **root** and the root password configured during installation.
**1) Assign interfaces**
   1. **Enter an option:** 1
   2. **Do you want to configure LAGGs now?** N
   3. **Do you want to configure VLANs now?** N
   4. Locate the MAC addresses for the virtual networks created earlier
   5. Enter the WAN interface name which matches the MAC address shown in OPNsense
   6. Enter the LAN interface name which matches the MAC address shown in OPNsense
   7. Press Enter again to skip the optional interface assignment
**2) Set interface IP address**
   1. **Enter an option:** 2
   2. Select the LAN interface
   3. **Configure IPv4 address LAN interface via DHCP?** N
   4. Enter the desired LAN IPv4 address (e.g. 192.168.1.1)
   5. Enter the desired LAN IPv4 subnet bit count (e.g. 24)
   6. Answer IPv6 questions based on personal preference
   7. **Do you want to enable the DHCP server on LAN?** y
   8. **Enter the start address of the IPv4 client address range** (e.g. 192.168.1.50)
   9. **Enter the end address of the IPv4 client address range** (e.g. 192.168.1.100)
   10. **Do you want to change the web GUI protocol from HTTPS to HTTP?** N
   11. **Do you want to generate a new self-signed web GUI certificate?** y
   12. **Restore web GUI access defaults?** y

## Issues
* Unable to access the web GUI using a virtual machine connected to the LAN network.
  * Temporary solution: Rebooting the OPNsense VM allowed me to access the web GUI.

### Desktop OS

### Server OS

### Kali Linux

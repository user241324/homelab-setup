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

# Creating the virtual firewall/router
1. Acquire the .iso
2. Create a new virtual machine
3. Review the configuration prior to installation (BIOS/UEFI, Networks, Storage)

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
      1. Disable DHCPv4 (Uncheck the **Enable DHCPv4** box). The goal is that OPNsense will handle DHCP configuration
      2. Make a note of the **IPv4 Network:** (for example, 192.168.100.0/24)

## Acquiring ISOs

### Virtual Firewall

### Desktop OS

### Server OS

### Kali Linux

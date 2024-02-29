# Proxmox macOS GPU Acceleration Configuration (Personal Reference)

This repository houses my personal configuration file for setting up a macOS virtual machine on Proxmox VE with GPU acceleration. It's specifically tailored for a system equipped with an AMD Ryzen 7 5800X CPU and an AMD Radeon RX 6600 XT GPU, enabling GPU passthrough for enhanced graphics performance in macOS VMs.

## Disclaimer

This setup works on **my system** but may not work for yours as-is. Consider this repository as a reference or a starting point for your own configuration. It's primarily here for me to easily replicate my setup or make adjustments if needed in the future.

### Configuration File Location

Ensure you place the `.conf` file in the following directory:

/etc/pve/qemu-server/


### `.conf` File Overview

Here's the core of my macOS VM configuration with GPU acceleration:

```plaintext
agent: 1
args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -global nec-usb-xhci.msi=off -global ICH9-LPC.acpi-pci-hotplug-with-bridge-support=off -cpu Haswell-noTSX,vendor=GenuineIntel,+invtsc,+hypervisor,kvm=on,vmware-cpuid-freq=on
balloon: 0
bios: ovmf
boot: order=virtio0
cores: 8
cpu: host
efidisk0: local-lvm:vm-103-disk-0,efitype=4m,size=4M
hostpci0: 0000:0a:00
machine: q35
memory: 16384
meta: creation-qemu=7.2.0,ctime=1681501041
name: Sonoma
net0: vmxnet3=(MAC ADDRESS),bridge=vmbr0
numa: 0
ostype: other
scsihw: virtio-scsi-pci
smbios1: [SOMETHING]
sockets: 1
usb0: [SOMETHING]
vga: none
virtio0: local-lvm:vm-103-disk-1,cache=unsafe,discard=on,size=250G
vmgenid: [SOMETHING]
```

### System Requirements and Notes

- **CPU:** AMD Ryzen 7 5800X
- **GPU:** AMD Radeon RX 6600 XT (for passthrough)

This configuration is based on my hardware setup. Adjustments may be necessary to match your system's specifications, especially the GPU passthrough settings.

### Installation

1. **Clone or download this repository** to your Proxmox VE host for easy access.
2. **Copy the `.conf` file** to `/etc/pve/qemu-server/`, replacing `<VMID>` with your actual VM ID.
3. **Customize the configuration** as needed, particularly the `hostpci0` line for your GPU's PCI address.
4. **Restart Proxmox VE** or the VM to apply your changes.

### Usage as a Reference

Feel free to use this configuration as a reference for setting up your own macOS VM with GPU acceleration in Proxmox VE. Modifications will likely be necessary to align with your hardware and requirements.

### Support and Contributions

Given the personal nature of this repository, I might not be able to provide support or guidance on adapting this setup to different systems. However, I welcome insights and suggestions for improvements.

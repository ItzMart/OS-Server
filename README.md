# Setting Up a Windows 10 VM with QEMU and noVNC

This guide will walk you through setting up a Windows 10 virtual machine using QEMU, noVNC, and other essential tools.

## Prerequisites

Ensure you have the following packages installed:

```bash
sudo apt update && sudo apt install tigervnc-standalone-server qemu-system-x86 firefox openbox neofetch kitty
```

## Setup noVNC

Clone the noVNC repository and start the VNC server:

```bash
git clone https://github.com/novnc/noVNC.git
cd noVNC/
sudo vncserver -SecurityType none -xstartup "openbox" -rfbport 5080
sudo ./utils/novnc_proxy --vnc 127.0.0.1:5080 --listen localhost:8080
```

## Prepare the VM Environment

Kill any running instances of Firefox, create a directory for the Windows 10 VM, and prepare the virtual hard disk:

```bash
killall firefox
mkdir win10
cd win10
qemu-img create hdd.img 12G
```

## Move the Windows ISO

Move the Windows 10 ISO to the VM directory:

```bash
cd
ls
cd Downloads
mv Win10_22H2_English_x64v1.iso ~/win10/Windows.iso
```

## Start the Virtual Machine

Navigate to the VM directory and start the VM using QEMU:

```bash
cd
cd win10
ls
qemu-system-x86_64 --enable-kvm -m 3G -smp 2 -pflash /usr/share/OVMF/OVMF_CODE.fd --hdd hdd.img --cdrom Windows.iso
```

## Accessing the VM

You can access the VM using noVNC by navigating to `http://localhost:8080` in your web browser.

## Additional Information

- **neofetch**: A command-line system information tool.
- **kitty**: A GPU-based terminal emulator.

This setup provides a lightweight and efficient way to run a Windows 10 VM with a browser-based VNC viewer.

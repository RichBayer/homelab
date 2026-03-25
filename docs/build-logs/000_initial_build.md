# Homelab Build Log

## Project Goal

Build an enterprise-grade nested Proxmox homelab for CompTIA Linux+ practice, Ansible automation, and a portfolio that demonstrates real-world sysadmin skills.

---

## Hardware (Lenovo Legion Desktop)

- CPU: AMD Ryzen 7 5800X (16 threads)
- RAM: 32 GB
- GPU: RTX 3060 (12 GB)
- Motherboard: Lenovo 3716 (B550 chipset)

### Storage (as of December 2025)
- 256 GB NVMe: Windows 11 boot
- 2 TB NVMe: personal files and media
- 1 TB SATA SSD: dedicated homelab storage
- 4 TB USB HDD: backups and ISO storage

---

## Remote Access Devices

- Lenovo Yoga laptop (Tailscale access)
- Galaxy S24 (Termius SSH client)

---

## Phase 0 – Hardware Prep (Dec 5, 2025)

Prepared the system for homelab use:

- Installed new 2 TB NVMe drive
- Migrated personal files off the 1 TB SATA SSD
- Wiped the SATA SSD to dedicate it fully to lab storage

---

## Phase 1 – Bare-Metal Attempt (Abandoned)

Initial plan was to install Proxmox directly on hardware using a dual-boot setup.

### Issues Encountered

- Inconsistent network detection during install
- Risk of selecting the wrong disk during installation
- Bootloader conflicts with Windows
- No way to access the lab while booted into Windows

### Decision (Dec 12, 2025)

Pivoted to a nested virtualization approach.

---

## Phase 2 – Nested Proxmox Setup (Dec 14, 2025)

Created a Proxmox VM inside VMware Workstation Pro.

### VM Configuration

- VMware Workstation Pro
- Guest OS: Debian 12
- 20 GB RAM
- 8 vCPU
- 100 GB virtual disk (thin provisioned)
- Raw passthrough of 1 TB SATA SSD
- Bridged networking
- Nested virtualization enabled

### Installation

- Installed Proxmox VE 8.3
- Configured static IP:
  - 192.168.1.149/24
  - Gateway: 192.168.1.1

### Initial Access

- Web UI: https://192.168.1.149:8006
- Root SSH configured using existing ed25519 key

---

## Phase 3 – Initial Issues and Troubleshooting

### Problems

- DNS resolution failures (`Temporary failure in name resolution`)
- `tailscaled` service not running

### Root Cause

- Tailscale installed using static binaries
- No systemd service → no automatic startup
- DNS pointing to Tailscale (100.100.100.100) without the service running

### Temporary Fix

Manually set DNS:

    echo "nameserver 8.8.8.8" > /etc/resolv.conf
    echo "nameserver 1.1.1.1" >> /etc/resolv.conf

---

## Phase 4 – Security Hardening

### User Setup

    adduser richb
    usermod -aG sudo richb
    apt install sudo

- Transitioned to non-root workflow using `richb` + sudo

### SSH Hardening

- Disabled root login:
  PermitRootLogin no

- Restarted SSH service:

    systemctl restart ssh

### DNS Protection (Temporary Measure)

    chattr +i /etc/resolv.conf

This prevented DNS changes but was later identified as too rigid for a dynamic lab environment.

---

## Phase 5 – Tailscale Proper Installation (Dec 14–15)

Replaced static binary install with official Debian package.

### Install

    curl -fsSL https://pkgs.tailscale.com/stable/debian/trixie.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
    curl -fsSL https://pkgs.tailscale.com/stable/debian/trixie.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
    apt update
    apt install tailscale

### Start Service

    tailscale up

### Results

- systemd service created and enabled
- Magic DNS functioning
- Node reachable remotely via Tailscale

---

## Remote Access Verification

Confirmed access from:

- Windows host (local and remote)
- Lenovo Yoga laptop
- Galaxy S24 via Termius SSH

---

## Phase 6 – Final Hardening and Stabilization (Dec 22, 2025)

### Completed Work

- Enforced key-only SSH authentication
- Disabled password authentication
- Fully disabled root SSH login
- Cleaned Proxmox repositories (removed enterprise repo warnings)
- Verified stable 24/7 remote access via Tailscale

---

## Proof Screenshots

### VMware VM Configuration
![VMware Proxmox VM settings](../screenshots/milestone-1/01-vmware-proxmox-vm-settings.png)

### Proxmox Console (VMware)
![Proxmox console in VMware](../screenshots/milestone-1/02-proxmox-console-in-vmware.png)

### Proxmox Web Dashboard
![Proxmox web dashboard](../screenshots/milestone-1/03-proxmox-web-dashboard.png)

### Tailscale Status
![Tailscale combined status](../screenshots/milestone-1/04-tailscale-combined.png)

### resolv.conf Immutable
![resolv.conf immutable](../screenshots/milestone-1/05-resolv-conf-immutable.png)

### SSH Hardening + Magic DNS
![SSH hardening and MagicDNS proof](../screenshots/milestone-1/06-ssh-hardening-and-magicdns.png)

---

## Current State

- Nested Proxmox VE 8.3 fully operational
- Secure SSH configuration in place (key-based only)
- Tailscale providing stable remote access
- Base platform ready for service deployment

---

## Next Step

Rocky Linux 9 VM (first workload server)

# Homelab Build Log

## Status

Milestone 1 complete as of December 22, 2025.

This document covers the initial build of the homelab environment, including:

- hardware preparation  
- Proxmox installation (nested)  
- networking setup  
- Tailscale integration  
- SSH hardening and access control  

Later phases (services, monitoring, automation, etc.) will be documented in future build logs.

---

## Project GoalBuild an enterprise-grade nested Proxmox homelab for CompTIA Linux+ practice, Ansible automation, and a standout GitHub portfolio demonstrating real-world sysadmin skills.

---

## Hardware (Lenovo Legion Desktop)

- CPU: AMD Ryzen 7 5800X (16 threads)
- RAM: 32 GB
- GPU: RTX 3060 12 GB
- Motherboard: Lenovo 3716 (B550 chipset)

### Storage (as of December 2025)
- 256 GB NVMe: Windows 11 boot
- 1 TB SATA SSD: Dedicated lab storage
- 2 TB Samsung 990 PRO NVMe: Windows files/media
- 4 TB USB HDD: Backups and ISOs

---

## Remote Access Devices

- Lenovo Yoga laptop (Tailscale)
- Galaxy S24 (Termius SSH)

---

## Phase 0 – Hardware Prep (Dec 5, 2025)

Freed the 1 TB SATA SSD for lab use:

- Installed new 2 TB NVMe
- Migrated personal data
- Wiped SATA SSD for homelab

---

## Phase 1 – Bare-Metal Attempts (Abandoned)

Tried dual-boot Proxmox.

### Issues Encountered
- USB install networking failures
- Installer selecting wrong disks (risk to Windows NVMe)
- Boot conflicts and instability
- No remote access when Windows was running

### Decision (Dec 12, 2025)

Pivoted to **nested Proxmox in VMware**.

### Reasons
- Windows always available for family use
- Full remote access via Tailscale
- No bootloader conflicts
- Near bare-metal performance with nested virtualization

---

## Phase 2 – Nested Proxmox Setup (Dec 14, 2025)

### VM Configuration

- VMware Workstation Pro
- Guest OS: Debian 12
- 20 GB RAM
- 8 vCPU
- 100 GB disk (thin provisioned)
- Raw passthrough of 1 TB SATA SSD
- Bridged networking (initially)
- Nested virtualization enabled

### Install Details

- Static IP: 192.168.1.149/24
- Gateway: 192.168.1.1

### Post-Install

- Proxmox web UI available at: https://192.168.1.149:8006
- Passwordless root SSH configured using existing ed25519 key

---

## Phase 3 – Initial Issues and Troubleshooting

### Problems

- DNS resolution failures (`Temporary failure in name resolution`)
- `tailscaled` service missing

### Root Cause

- Tailscale was installed using static binaries
- No systemd service → no auto-start
- DNS pointed to Tailscale (100.100.100.100) but service was not running

### Temporary Fix

    echo "nameserver 8.8.8.8" > /etc/resolv.conf
    echo "nameserver 1.1.1.1" >> /etc/resolv.conf

---

## Phase 4 – Security Hardening

### User Setup

    adduser richb
    usermod -aG sudo richb
    apt install sudo

- Adopted non-root workflow (`richb` + sudo)

### SSH Hardening

- Disabled root login:
  PermitRootLogin no

- Restarted SSH:
    systemctl restart ssh

### DNS Protection (Later Adjusted)

    chattr +i /etc/resolv.conf

Note: This prevented unwanted overwrites but later caused issues when network changes required dynamic DNS updates.

---

## Phase 5 – Permanent Tailscale Implementation (Dec 14–15)

### Install

    curl -fsSL https://pkgs.tailscale.com/stable/debian/trixie.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
    curl -fsSL https://pkgs.tailscale.com/stable/debian/trixie.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
    apt update
    apt install tailscale

### Start Service

    tailscale up

### Results

- systemd service created and enabled
- Magic DNS functional
- Node reachable via Tailscale

---

## Remote Access Verification

- Windows host (local + remote)
- Lenovo Yoga laptop (SSH + web UI)
- Galaxy S24 via Termius SSH

---

## Phase 6 – Final Hardening and Milestone 1 Completion (Dec 22, 2025)

### Completed Work

- Full key-only SSH authentication
- Disabled password authentication completely
- Root SSH login fully blocked
- Cleaned Proxmox repositories (removed enterprise warnings)
- Verified stable 24/7 remote access via Tailscale

---

## Proof Screenshots

### VMware Workstation VM Settings
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

## Current Status (Dec 22, 2025)

- Nested Proxmox VE 8.3 fully operational
- Tailscale installed with automatic startup
- Secure SSH workflow in place (key-based only)
- Remote access confirmed across all devices
- Documentation and screenshots complete

---

## Next Step

👉 Milestone 2: Rocky Linux 9 cloud-init template

This log will continue as the lab evolves.

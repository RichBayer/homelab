# Homelab – Rich Bayer

Former U.S. Army helicopter mechanic transitioning into IT, focused on Linux systems administration and cloud infrastructure.

This repo documents a hands-on homelab I’m building to develop real-world skills for a Linux/sysadmin role. The goal isn’t just to stand things up, but to understand how systems behave, break, and get fixed.

---

## 🎯 Career Direction

- CompTIA Linux+ (XK0-006)
- Junior Linux / Sysadmin / Cloud Support role
- Target: $75k–$90k remote role
- Timeline: 2026

---

## 🧠 What This Lab Is

This isn’t a checklist lab.

The idea is to simulate a small company environment where I can:

- administer Linux systems  
- troubleshoot real problems  
- manage users, permissions, and services  
- deploy and maintain applications  
- build and automate infrastructure  
- document everything as I go  

The focus is on learning how systems actually behave, not just getting them running.

---

## 🏗️ Current Architecture

- Windows 11 host (Lenovo Legion)
- VMware Workstation Pro
- Proxmox VE 8.3 (nested)
- Tailscale (MagicDNS + SSH)

This setup lets me:

- keep Windows available at all times  
- access the lab remotely from anywhere  
- work directly inside the environment without rebooting  
- experiment freely without risking my main system  

---

## 💻 Hardware

- Ryzen 7 5800X (16 threads)
- 32 GB RAM
- RTX 3060 (12 GB)

Storage:
- 256 GB NVMe (Windows boot)
- 2 TB NVMe (personal files)
- 1 TB SATA SSD (lab)
- 4 TB external HDD (backups)

---

## 🚀 Direction / Roadmap

The lab is being built in stages, with each step documented.

Current focus:

- stable Proxmox base
- secure remote access (Tailscale + SSH)
- clean, repeatable workflow

Next steps:

- Rocky Linux server (first real workload)
- web server + database
- internal file server (Samba, users, permissions)
- monitoring (Prometheus + Grafana)
- Ansible automation
- backup + recovery
- self-hosted portfolio site

---

## 📂 Repo Layout

docs/
  build-logs/       → what was done and when  
  architecture/     → design decisions and layout  
  procedures/       → repeatable steps  
  troubleshooting/  → problems and fixes  
  screenshots/      → proof and visuals  

scripts/            → automation (later)  
prompts/            → workflow continuity  

---

## 📘 Documentation

Build log:
- docs/build-logs/000_initial_build.md

Screenshots:
- docs/screenshots/milestone-1/

I try to commit regularly so progress is visible and not reconstructed later.

---

## 🧪 What This Shows

- Linux administration fundamentals  
- SSH hardening and secure access  
- network troubleshooting across multiple layers  
- virtualization and system design  
- ability to track down and fix real issues  
- disciplined documentation  

---

## 🔁 Operational Simulation (Planned)

This lab isn’t just about building systems—it’s about operating them.

Planned additions:

- intentional service failures  
- simulated “user problems” (site down, login issues, etc.)  
- troubleshooting using logs and system state  
- repeatable failure scenarios  

Longer term, I want to introduce a simple system that can:

- inject failures  
- simulate tickets  
- create real troubleshooting scenarios on demand  

The goal is to get comfortable diagnosing problems, not just configuring systems.

---

## 📬 Current State

The base platform is built, secured, and accessible remotely.

Next phase is adding real services and turning this into a working environment instead of just infrastructure.

---

## 📬 Notes

This is an evolving project. I’m building it out step-by-step and documenting everything along the way.

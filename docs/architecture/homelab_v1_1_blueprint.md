# Homelab V1.1 Blueprint – BayerTech Lab Environment

---

# 🎯 Purpose

This homelab simulates a small-to-medium business Linux infrastructure for:

- Linux system administration training  
- CompTIA Linux+ (XK0-006) preparation  
- Real-world troubleshooting  
- Chaos engineering and fault injection  
- Portfolio development  

---

# 🧠 Design Philosophy

This lab is:

- Small enough to manage  
- Complex enough to simulate real systems  
- Built with interdependent services  
- Designed for controlled failure and recovery  
- Portable and reproducible across hardware environments  

---

# 🏢 Lab Identity

- Organization: BayerTech Solutions  
- Environment Type: Internal IT Infrastructure  
- Hypervisor (Current): VMware Workstation  
- Future Target: Dell PowerEdge R730  

---

# 🔑 Core Design Principle

> “Build once. Move anywhere.”

---

# 🖥️ VM Architecture

## Nodes

- client01 → Admin workstation  
- web01 → Web server  
- files01 → File & backup server  
- mon01 → Monitoring server  
- infra01 → DNS / infrastructure server  
- legacy01 → Optional degraded system  

---

# 🌐 Network Design

## Internal Network

192.168.50.0/24  

## Static IP Assignments

- client01 → 192.168.50.10  
- web01 → 192.168.50.20  
- files01 → 192.168.50.30  
- mon01 → 192.168.50.40  
- infra01 → 192.168.50.50  
- legacy01 → 192.168.50.60  

---

# 📛 Naming Rules

- Hostnames must never change  
- Naming must remain consistent across all configs  
- Avoid environment-specific naming  

---

# 💾 Storage Design

## VM Storage Location

G:\homelab\vms\  

## Structure

vms/
├── client01/
├── web01/
├── files01/
├── mon01/
├── infra01/
├── legacy01/

---

## Rules

- Each VM stored in its own directory  
- Thin provisioning preferred  
- No host-specific dependencies inside VMs  

---

# 👥 User & Group Model

## Users

- patrice (management)  
- abigail (web)  
- frank (engineering)  
- pete (engineering)  
- karen (management)  
- jerry (ops)  
- barbara (ops)  
- carmen (web)  
- greg (engineering)  
- johnny (ops)  

### Service Accounts

- backupsvc  
- websvc  

---

## Groups

- engineering  
- web  
- ops  
- management  
- shared  
- backup  

---

# 📁 Filesystem Design

## Root Path

/srv/company/

## Structure

- engineering/  
- web/  
- ops/  
- management/  
- shared/  
- backups/  

---

## Permissions Model

- Department directories → 770  
- Shared directory → 775 + sticky bit  
- Backups → restricted access  

---

## Advanced Controls

- setgid for group inheritance  
- ACLs for cross-team access  

---

# ⚙️ Service Architecture

## web01

- Apache or Nginx  
- Internal web content  

## files01

- File storage  
- Backup target  

## mon01

- Cron jobs  
- Health monitoring scripts  

## infra01

- DNS  
- Core infrastructure services  

---

# 🔗 Dependency Model

infra01  
↓  
web01 / files01  
↓  
mon01  
↓  
client01  

---

# 💣 Chaos Engineering Strategy

## Goal

Develop 200+ realistic fault scenarios  

---

## Fault Tiers

Tier 1 → Basic issues  
Tier 2 → Intermediate  
Tier 3 → Multi-system  
Tier 4 → Incident scenarios  

---

## Script Design

- Randomized naming (fault_xxxx.sh)  
- Hidden index mapping  
- Paired reset scripts  

---

# 🔁 Portability & Migration Strategy

## Core Rules

- No host-specific dependencies  
- No hypervisor-specific reliance  
- All configs reproducible  

---

## Externalized State

All system design must be stored in repo:

- users & groups  
- directory structure  
- permissions  
- service configs  

---

## Migration Workflow

1. Copy VM directories  
2. Import into new hypervisor  
3. Boot systems  
4. Validate networking  

---

## Success Condition

> Migration requires NO rebuild  

---

# 🧪 Training Capabilities

This lab is designed to fully support all domains of the CompTIA Linux+ XK0-006 exam, including:

## System Management
- Process management  
- Service management (systemctl)  
- System monitoring  

## Security
- File permissions and ownership  
- ACLs  
- Authentication concepts  
- Basic system hardening  

## Scripting & Automation
- Bash scripting fundamentals  
- Cron jobs  
- Task automation  

## Troubleshooting
- Service failures  
- Permission issues  
- Network issues  
- Log analysis  
- Multi-system failure scenarios  

## Networking
- IP configuration  
- DNS resolution  
- Connectivity troubleshooting  

## Storage
- Disk management  
- File systems  
- Mounts  
- Backup and recovery  

---

## Objective

Ensure the environment provides:

> Real-world, repeatable scenarios that reinforce both exam success and practical system administration skills.

---

# 🧠 Guiding Principle

> “Train like it’s broken. Build like it will move.”

---

# 🔚 End of Document
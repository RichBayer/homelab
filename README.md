# Enterprise Homelab Portfolio - Rich Bayer

Former military helicopter mechanic transitioning to **Junior Linux SysAdmin / Cloud Support**.

### Goals
- Pass CompTIA Linux+ by end of February 2026
- Land remote junior role ($55k–$75k) by May 2026
- Build a public GitHub portfolio that forces interviews

### Hardware
- **Lenovo Legion** (Windows 11 host): Ryzen 7 5800X, 32GB RAM, RTX 3060
  - Storage: 256GB NVMe (boot), 2TB NVMe (games/files), 1TB SATA SSD (VM storage), 4TB USB (backups)
- **Lenovo Yoga** (daily driver): Tailscale remote access

### Architecture Decision (Dec 12 2025)
Abandoned bare-metal dual-boot → Entire lab runs as **nested Proxmox VE VM** under VMware Workstation Pro on Windows host.

**Reasons**: Family uninterrupted Windows access, copy-paste workflow, 24/7 Tailscale remote, zero boot issues, near-bare-metal performance.

### Planned Milestones
| #  | Component                              | Purpose                                      |
|----|----------------------------------------|----------------------------------------------|
| 1  | Nested Proxmox + Tailscale             | 24/7 remote access (current)                 |
| 2  | Rocky Linux 9 cloud-init template      | Fast, repeatable deployments                 |
| 3  | Bastion LXC                            | Hardened, key-only SSH entry point           |
| 4  | OPNsense firewall VM                   | Perimeter security + routing                 |
| 5  | Pi-hole + Unbound + Samba LXC          | Network-wide DNS, ad-blocking, file sharing  |
| 6  | Prometheus + Node Exporter + Grafana   | Full observability stack                     |
| 7  | Rocky Linux Workstation VM             | Ansible control node                         |
| 8  | Ansible playbooks                      | Idempotent configuration of everything       |
| 9  | Daily backup script + rotation         | Disaster recovery to 4TB USB                 |
| 10 | Final polish + Loom video + rebuild guide | One-click reproducible lab                |
| 11 | Personal static portfolio website (Nginx) | Self-hosted resume/site with real traffic monitoring |

Detailed build log → [docs/BUILD_LOG.md](docs/BUILD_LOG.md)  
Screenshots → [screenshots/](screenshots/)

Methodical nightly commits guaranteed.

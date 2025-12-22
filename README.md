# Homelab Portfolio – Rich Bayer

Former military helicopter mechanic transitioning into IT.  
Goal: Pass CompTIA Linux+ by late February 2026 and land a remote junior Linux/sysadmin or cloud support role ($55–75k) by May 2026.  
This public repo is built to showcase real, hands-on work that gets interviews.

Hardware
- Main host: Lenovo Legion (Windows 11)  
  Ryzen 7 5800X, 32 GB RAM, RTX 3060  
  Storage: 256 GB NVMe (boot), 2 TB NVMe, 1 TB SATA SSD (VMs), 4 TB USB (backups)
- Daily driver: Lenovo Yoga laptop – used for remote Tailscale access

Architecture (decided Dec 12 2025)
Ditched the original bare-metal dual-boot idea. Everything now runs as a single nested Proxmox VE 8.3 VM under VMware Workstation Pro on the Windows host.

Why this way?
- Family keeps uninterrupted Windows access
- Full copy-paste between host and VMs
- True 24/7 remote access via Tailscale
- No boot conflicts or hardware passthrough headaches
- Near bare-metal performance with nested virtualization

Planned Milestones

1. Nested Proxmox + Tailscale – 24/7 remote access (complete Dec 22 2025)
2. Rocky Linux 9 cloud-init template – fast, repeatable VM deployments
3. Bastion LXC – hardened, key-only SSH jump host
4. OPNsense firewall VM – perimeter security and routing
5. Pi-hole + Unbound + Samba LXC – network-wide ad-blocking, recursive DNS, file sharing
6. Prometheus + Node Exporter + Grafana – full monitoring and alerting
7. Rocky Linux Workstation VM – dedicated Ansible control node
8. Ansible playbooks – idempotent configuration of the entire lab
9. Daily backup script + rotation – disaster recovery to 4 TB USB drive
10. Final polish – Loom walkthrough video + one-click rebuild guide
11. Personal static portfolio site (Nginx) – self-hosted resume with real traffic monitoring

Detailed day-by-day build log → docs/BUILD_LOG.md  
All screenshots → screenshots/  

I commit regularly (usually same or next day) so progress is transparent.

Thanks for checking it out!

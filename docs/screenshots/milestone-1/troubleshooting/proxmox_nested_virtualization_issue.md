# Proxmox Nested Virtualization Issue (VMware + WSL Conflict)

## Summary

Attempted to run Proxmox VE as a nested hypervisor inside VMware Workstation while also running WSL2 on the Windows host.

This configuration failed due to a conflict between:

- Windows Hypervisor Platform, which is required for WSL2
- VMware nested virtualization requirements, which are required to run Proxmox as a hypervisor inside VMware

As a result, the homelab architecture is being temporarily adjusted.

---

## Symptoms

During troubleshooting and recovery work, the following issues were encountered:

- VMware reported: "Failed to start the virtual machine"
- The VMX file was briefly reported as corrupt after manual edits, caused by a duplicate configuration entry
- WSL stopped launching after Windows hypervisor components were disabled
- After WSL was restored, VMware could no longer start the Proxmox VM
- WSL also reported an `/etc/fstab` mount failure caused by an invalid Linux-style UUID mount entry that did not belong in WSL

---

## Root Cause

The key failure from `vmware.log` was:

    ULM: Failed to set up partition, res 0xc0350005
    Module 'ULM' power on failed.

This indicates that VMware could not create the required virtualization partition while Windows Hypervisor Platform was active.

In practical terms:

- WSL2 requires Hyper-V / Windows Hypervisor Platform
- VMware can run with Hyper-V present, but nested virtualization becomes limited or unavailable
- Proxmox, when hosted inside VMware, requires nested virtualization
- Therefore, WSL2 and nested Proxmox-on-VMware conflict on this host architecture

---

## Architecture at Time of Failure

At the time of failure, the system architecture was:

    Windows 11 Host
     → WSL2 Ubuntu
     → VMware Workstation
       → Proxmox VE
         → Intended guest VMs

This meant both NeuroCore and the Homelab depended on the same host virtualization stack, but in different ways.

---

## Troubleshooting Actions Taken

The following recovery and validation steps were performed:

1. Re-enabled required Windows virtualization features after they had been disabled during homelab network troubleshooting
2. Restored WSL functionality by turning the Windows hypervisor back on
3. Confirmed that WSL could launch again
4. Identified and corrected an invalid `/etc/fstab` entry inside WSL that attempted to mount a Linux UUID-based ext4 filesystem
5. Confirmed that WSL launched cleanly after the `fstab` fix
6. Attempted to restore Proxmox startup inside VMware
7. Updated the `.vmx` configuration to test nested virtualization compatibility settings
8. Corrected a duplicate `vhv.enable` entry that caused a temporary VMX corruption warning
9. Reviewed `vmware.log` to identify the actual failure point
10. Confirmed that the final blocker was a Hyper-V / nested virtualization limitation, not a simple VM configuration typo

---

## Key Constraint

The current host must support both of the following:

- NeuroCore in WSL2
- Homelab virtualization

WSL2 requires the Windows hypervisor stack.

Proxmox running inside VMware requires nested virtualization.

On this Windows host, once Hyper-V / Windows Hypervisor Platform is enabled for WSL2, VMware cannot reliably provide the nested virtualization required by Proxmox.

That makes this a platform limitation, not just a misconfiguration.

---

## Resolution / Decision

Proxmox will be temporarily paused in the current Legion workstation environment.

The Homelab will continue using:

    VMware Workstation → direct Linux virtual machines

This preserves:

- NeuroCore functionality in WSL2
- a usable homelab environment
- continued Linux administration and troubleshooting practice
- a clean path forward without repeatedly fighting the same host limitation

This is a temporary architectural pivot, not a permanent abandonment of Proxmox.

---

## Updated Working Architecture

The active working architecture is now:

    Windows 11 Host
     ├── NeuroCore (WSL2)
     └── VMware Workstation
          ├── Linux practice VM(s)
          ├── future service VM(s)
          └── future troubleshooting / ticket simulation VM(s)

Proxmox is retained as part of the broader learning path, but it is not the active virtualization layer on this host at this time.

---

## Future Plan

Proxmox will be reintroduced later on dedicated hardware.

Planned future target:

- Dell PowerEdge R730
- Proxmox installed on bare metal

That future design will remove the Windows Hyper-V / VMware nested virtualization conflict and allow Proxmox to function in the role it was originally intended to fill.

---

## Lessons Learned

- Nested virtualization under Windows Hyper-V has real limitations
- Host-level virtualization changes affect both WSL and VMware
- Troubleshooting must happen at the correct layer: host, hypervisor, guest, or service
- A shared system state document is necessary when two major projects share one host and are expected to integrate later
- Architectural pivots should be documented clearly so the same dead-end is not repeated later

---

## Status

Current status is:

- WSL restored and functioning
- NeuroCore operational again
- Proxmox VM retained but paused
- Homelab pivoted to VMware-based VM hosting for the current phase
- documentation updated to reflect the new direction
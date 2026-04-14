# 001 – Homelab Foundation

## Objective

Establish a clean, structured foundation for the homelab environment aligned with:

- VMware-based virtualization (no nested Proxmox)
- NeuroCore-integrated filesystem layout
- Future migration to dedicated server infrastructure (R730)
- XK0-006 exam-aligned training environment

---

## Starting State

- No active homelab environment
- Previous homelab attempt abandoned
- NeuroCore system already established at:

/mnt/g/ai/

---

## Actions Taken

### 1. Created New Homelab Repository

Location:

/mnt/g/ai/projects/homelab

Commands:

```bash
cd /mnt/g/ai/projects
mkdir homelab
cd homelab
git init
```

---

### 2. Established Base Repository Structure

Created directories:

```bash
docs/
├── architecture/
├── build/
├── chaos/
├── operations/

scripts/
├── faults/
├── resets/
├── utilities/

build-logs/
```

---

### 3. Created Homelab System Prompt

Defined strict operating rules including:

- No guessing system state
- Step-by-step execution model
- Architecture-first design
- Reproducibility and portability requirements

Location:

docs/architecture/homelab_system_prompt.md

---

### 4. Created Homelab V1.1 Blueprint

Defined full system design including:

- VM architecture
- Network layout
- User and group model
- Filesystem structure
- Chaos engineering strategy
- Migration plan to future server

Location:

docs/architecture/homelab_v1_1_blueprint.md

---

### 5. Created Validated Repository Map

Captured real filesystem structure:

- Verified directory layout
- Ensured no assumptions in documentation
- Established repo as source of truth

Location:

docs/architecture/repo_map.md

---

## Key Decisions

### 1. Storage Architecture

- NeuroCore → /mnt/g/ai
- Homelab repo → /mnt/g/ai/projects/homelab
- VM storage → G:\homelab\vms

Reason:

- High-speed NVMe storage
- Clean separation of systems
- No interference between AI and lab environments

---

### 2. Virtualization Strategy

- VMware Workstation selected
- Proxmox nested virtualization abandoned

Reason:

- Compatibility issues with WSL/Hyper-V
- Simplified architecture
- Faster path to functional training environment

---

### 3. Lab Design Approach

- Small-business simulation (BayerTech Solutions)
- Multi-VM architecture with dependencies
- Real user and group modeling
- Chaos engineering integration planned

---

## Validation

- Repository created successfully
- Directory structure verified with `tree`
- System prompt, blueprint, and repo map created
- Files placed in correct architecture locations
- No conflicts with existing NeuroCore environment
- Clean separation between AI system and lab infrastructure

---

## Result

A fully defined and structured homelab foundation ready for:

- VM deployment
- user and permission modeling
- service configuration
- fault injection development

---

## Next Step

Begin VM creation:

client01 → Admin workstation

---

## Notes

This marks the transition from planning → execution.

All future work will follow:

- strict system prompt rules
- validated step-by-step implementation
- structured build logging
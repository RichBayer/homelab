# Homelab Prompting Strategy

---

# 🎯 Purpose

Ensure consistent, accurate continuation of homelab development across ChatGPT sessions.

Prevent:

- context loss  
- incorrect assumptions  
- architectural drift  

---

# 🧠 Session Start Workflow

When starting a new ChatGPT session:

## Step 1 — Paste Resume Prompt

Paste:

docs/ai-operations/resume_prompt.md

---

## Step 2 — Provide Required Documents

Paste or upload:

- docs/architecture/homelab_system_prompt.md  
- docs/architecture/homelab_v1_1_blueprint.md  
- docs/architecture/repo_map.md  
- latest build log from build-logs/  

---

## Step 3 — Provide Current System State (if needed)

Run:

```bash
tree -a -L 3
```

Paste output to reflect real system state.

---

## Step 4 — Give Instruction

Example:

"Continue homelab build. Begin client01 setup."

---

# ⚠️ Rules

- Never assume ChatGPT remembers previous sessions  
- Always provide system context  
- Always keep repo_map.md accurate  
- Always update build logs after meaningful work  
- Never allow guessing of system state  

---

# 🧭 Objective

Maintain:

- accuracy  
- consistency  
- reproducibility  
- clean architecture  

---

# 🧠 Philosophy

The system must behave the same way every time it is resumed.

---

# 🔚 End Document
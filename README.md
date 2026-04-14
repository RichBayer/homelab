# Homelab – BayerTech Lab Environment

## Overview

This repository contains a structured Linux homelab environment designed to simulate a real-world system administration environment.

The lab is built to support:

- CompTIA Linux+ (XK0-006) exam preparation  
- Practical Linux system administration training  
- Real-world troubleshooting scenarios  
- Chaos engineering and fault injection  

---

## Design Philosophy

This is not a collection of random VMs.

This lab is designed as a **small business infrastructure simulation**:

> BayerTech Solutions

The environment includes:

- Multiple Linux systems with defined roles  
- Real users, groups, and permissions  
- Interdependent services  
- Controlled failure scenarios  

---

## Architecture

The lab consists of the following systems:

- `client01` – Admin workstation  
- `web01` – Web server  
- `files01` – File and backup server  
- `mon01` – Monitoring system  
- `infra01` – DNS and infrastructure services  
- `legacy01` – Optional degraded system for troubleshooting  

---

## Key Features

- Structured repository-driven design  
- Full documentation of system architecture  
- Step-by-step build logs  
- Planned chaos engineering library (200+ scenarios)  
- Portable design for migration to dedicated server hardware  

---

## Repository Structure

- `docs/architecture/` → system design and blueprint  
- `docs/operations/` → user models and filesystem design  
- `docs/chaos/` → fault injection strategy and scenarios  
- `scripts/` → automation and fault scripts  
- `build-logs/` → step-by-step implementation history  

---

## Training Objective

The goal is not just to learn commands.

The goal is to:

> Develop real-world Linux troubleshooting ability through structured repetition and controlled failure.

---

## Current Status

Phase: Foundation Complete  

Next Step:

- Begin VM deployment (client01)

---

## Future Plans

- Full chaos engineering library  
- NeuroCore integration for automated fault injection  
- Migration to dedicated server infrastructure  

---

## Guiding Principle

> Train like it’s broken. Build like it will move.
# 🚀 Home Lab Infrastructure & Automation

Welcome to the central repository for my personal home lab. This repository houses the "Infrastructure as Code" (IaC), Docker Compose stacks, and automation scripts that power my headless Ubuntu server environment. 

Currently running a **Compute + DAS (Direct Attached Storage)** model, this lab is designed to be low-power, high-performance, and entirely modular.



---

## 🏗️ Architecture Overview

The core philosophy of this lab is separating compute from storage to avoid the "RAID Tax" of traditional NAS appliances. 

### 💻 Hardware Specs
| Component | Hardware / Details |
| :--- | :--- |
| **Compute Node** | GMKtec K8 Mini PC (Ryzen 8000-series, Headless) |
| **Storage Enclosure**| 4-Bay USB-C DAS (Direct Attached Storage) |
| **Storage Capacity** | 8TB Usable Pool (via MergerFS) + Dedicated Parity Drive |
| **Network** | Hardwired Ethernet |

### 🧩 Software Stack
* **OS:** Ubuntu Server 24.04 LTS (Bare Metal)
* **Storage Pooling:** MergerFS (Virtual unified drive)
* **Data Parity:** SnapRAID (Snapshot-based parity for disaster recovery)
* **Orchestration:** Docker & Docker Compose (Migrating to Kubernetes)
* **Remote Access:** SSH (Key-based authentication only) + VS Code Remote SSH

---

## ⚙️ Automation & `.bash_aliases`

To keep the Ubuntu environment clean and repeatable, all custom aliases and automation scripts are stored in this repository and dynamically injected into the server's session.

The core script is designed to be "dot-sourced" directly into the user's `~/.bashrc` via a dedicated `~/.bash_aliases` file. This prevents subshell isolation and loads all custom commands (like `dcup` for `docker-compose up -d`) into the active terminal immediately upon login.

```bash
# Example alias sourcing
if [ -f ~/homelab-repo/scripts/.bash_aliases ]; then
    . ~/homelab-repo/scripts/.bash_aliases
fi
📂 Repository Structure
/docker/ - Contains all docker-compose.yml stacks and .env templates.

/docker/plex/ - Hardware-accelerated media server.

/docker/nextcloud/ - Personal file synchronization and sharing.

/scripts/ - Bash automation, SnapRAID sync schedules, and backup utilities.

/k8s/ - (Work in Progress) Future Kubernetes manifests and Helm charts.

/config/ - Persistent configuration files mapped to Docker volumes.

🗺️ Roadmap
[x] Phase 1: Provision headless Ubuntu Server via SSH.

[x] Phase 2: Implement Docker Compose architecture for media and web apps.

[ ] Phase 3: Deploy MergerFS + SnapRAID for the USB-C storage pool.

[ ] Phase 4: Establish secure remote access (Zero Trust / Tailscale).

[ ] Phase 5: Migrate core services from Docker Compose to a lightweight Kubernetes distribution (K3s/MicroK8s).

Note: This repository is customized for my specific hardware and network. If you are cloning this for your own use, please review the .env.example files and replace the IP addresses, volume mappings, and PUID/PGID variables to match your system.

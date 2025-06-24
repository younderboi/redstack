# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Noctua is a modular red teaming stack built on Debian 12 and Ansible, designed for defensive security testing and penetration testing purposes. The project emphasizes source-first tooling, idempotent provisioning, and modular deployment models.

## Common Commands

### Ansible Playbook Execution
```bash
# Deploy full noctua stack to remote host
ansible-playbook playbooks/noctua.yml

# Deploy admin/desktop setup to local system
ansible-playbook playbooks/admin.yml

# Run specific roles with tags
ansible-playbook playbooks/noctua.yml --tags "core,dev"
ansible-playbook playbooks/noctua.yml --tags "red,AD"

# Limit execution to specific hosts
ansible-playbook playbooks/noctua.yml --limit noctua
ansible-playbook playbooks/admin.yml --limit admin

# Check what would be changed (dry run)
ansible-playbook playbooks/noctua.yml --check

# Run with increased verbosity
ansible-playbook playbooks/noctua.yml -vv
```

### Development and Testing
```bash
# Validate Ansible syntax
ansible-playbook --syntax-check playbooks/noctua.yml

# Test role dependencies
ansible-galaxy install -r requirements.yml

# List available hosts
ansible-inventory --list

# Ping all hosts
ansible all -m ping
```

## Architecture Overview

### Deployment Models
The project supports multiple deployment patterns:
- **Local monolith**: Full stack on single system
- **Headless node**: Remote system without GUI
- **Thin client/server**: GUI tools local, heavy tools remote
- **Hybrid**: Local tooling with remote pivot/jumpbox
- **Specialized nodes**: C2 servers, recon nodes, archival systems

### Directory Structure
- `playbooks/`: Main Ansible playbooks for different deployment targets
- `roles/`: Modular Ansible roles organized by function
- `inventories/`: Host inventory files (hosts.ini)
- `bin/`: Custom scripts and utilities
- `archive/`: Historical/backup configurations

### Role Categories
- **Core Environment**: networking, tmux, zsh, shell_utils, neovim
- **Language SDKs**: golang, python, python2, php, ruby_gem
- **Red Team Arsenal**: bloodhound, netexec, sliver, privesc, cracking, AD_tools
- **Desktop/GUI**: desktop, browsers, signal
- **Infrastructure**: docker, NFS, networking, pivot tools

### Key Design Principles
- Source-first tooling (built from source when possible)
- Idempotent provisioning via Ansible
- Modular, tag-based role selection
- Minimal base install - everything is opt-in
- Tools deployed to `/arsenal/` directory structure

### Host Configuration
- **admin**: Local admin system (127.0.0.1)
- **noctua**: Remote deployment target
- Configured in `inventories/hosts.ini`

### Role Dependencies
- Most roles are independent and can be run individually
- Core environment roles should be run before specialized tools
- Some roles have meta dependencies defined in `meta/main.yml`

## File Locations
- Ansible configuration: `ansible.cfg`
- Host inventory: `inventories/hosts.ini`
- Role tasks: `roles/[role_name]/tasks/main.yml`
- Role files: `roles/[role_name]/files/`
- Role metadata: `roles/[role_name]/meta/main.yml`
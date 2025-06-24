# Noctua

A source-readable, modular red teaming stack built on Debian 12 and Ansible.  
*(Eventually migrating to Void Linux...)*

Noctua is designed as a **rock-solid base** for surgical offensive operations.

Tools are built from source wherever possible, and provisioning is done cleanly via Ansible.

Ongoing work in progress — but already operational.

---

## 🎯 Goals

- Idempotent provisioning via Ansible
- Minimal base install — everything is opt-in
- Source-first tooling (wherever possible)
- Headless first

---

## 🧱 Deployment Models

Noctua can be deployed in an infite set of ways, but here's some examples:

- **Local monolith** — like a GUI Kali Linux

- **Headless node**
  - fully remote
  - no GUI tooling
  - RDP/VNC

- **Recon node**
  - Periodically scan and store stuff

- **C2 server node**

---

## 🔐 OPSEC & Security Philosophy

- **Bloat = attack surface** — nothing is installed without intent
- All tooling is opt-in and source-visible
- Most tools are built from source to enable auditing
- That said — current priority is OSCP completion, so OPSEC is *not* locked down yet

---

## 🛠️ Planned Features

- GitLab + artifact repository
- Basic EDR/defensive implements

---

**Very much WIP.**
If you like this, feel free to reach out.

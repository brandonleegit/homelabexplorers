# Challenge: Deploying Portainer on a Docker Host (Proxmox VM)

## 🛠️ Environment

- **Proxmox VE 8.1**
- **Ubuntu Server 22.04 LTS** (running as VM)
- **Docker 24.0.7**
- **Docker Compose Plugin 2.24.5**

## 📦 Goal

Install and configure Portainer using Docker Compose on a virtual machine hosted by Proxmox.

## ✅ Completed Steps

1. Created a VM in Proxmox with 2 vCPUs, 4GB RAM, and 32GB disk space.
2. Installed Docker and Docker Compose plugin on the VM.
3. Created a `docker-compose.yml` file for Portainer (see below).
4. Launched Portainer using `docker compose up -d`.
5. Accessed the Portainer UI via `https://<vm_ip>:9443` and created the admin account.

## 🔐 Note

At the first start, **there is no default username or password**. You are prompted to create the admin user and password on the first login screen.

## 📎 Useful Links

- [Portainer CE Documentation](https://docs.portainer.io/)
- [Docker Installation Guide for Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

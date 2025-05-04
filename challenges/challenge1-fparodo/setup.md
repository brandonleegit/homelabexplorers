Setup Instructions

Requirements:

    Proxmox VE installed on your server

    ISO for Ubuntu Server (or another preferred Linux distro)

    Basic knowledge of SSH and terminal
    

## Installation

✅ Step 1: Create a Virtual Machine for Docker in Proxmox

    Login to Proxmox Web UI

    Click Create VM

    Give it a name like docker-host

    Choose an OS (e.g., Ubuntu Server 22.04 LTS ISO)

    Configure:

        System: Default is fine

        Hard Disk: 32GB+ (depends on your needs)

        CPU: 2 Cores minimum

        Memory: 2GB+ recommended

        Network: Use default vmbr0 with VirtIO adapter

    Start the VM and complete the Ubuntu installation

    Once installed, SSH into the VM or use the console in Proxmox

✅ Step 2: Install Docker & Docker Compose

# Update system
sudo apt update && sudo apt upgrade -y

# Install Docker
curl -fsSL https://get.docker.com | sudo sh

# Enable Docker
sudo systemctl enable docker
sudo systemctl start docker

# Install Docker Compose v2 (plugin-based)
sudo apt install docker-compose-plugin -y

# Test installation
docker version
docker compose version

✅ Step 3: Create Docker Compose File for Portainer

    Create a directory:

mkdir -p ~/portainer && cd ~/portainer

    Create the docker-compose.yml:

version: '3.8'

services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: always
    ports:
      - "8000:8000"
      - "9443:9443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - portainer_data:/data

volumes:
  portainer_data:

    Start the service:

docker compose up -d

✅ Step 4: Access Portainer

Open your browser and go to:

https://<IP_OF_YOUR_VM>:9443

When you start Portainer for the first time, there is no default username or password.

✅ Instead, you'll be prompted to create an admin user. Here's what you'll see:

    A form asking for:

        Username (e.g., admin)

        Password

        Confirm Password

    After submitting, that becomes your login credentials.




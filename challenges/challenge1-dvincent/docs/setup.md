# Setup Instructions

## System Requirements
- Hardware requirements:
  - CPU: 2+ cores recommended
  - RAM: Minimum 2GB, 4GB+ recommended
  - Storage: 20GB+ free space for Docker images and container data
- Software requirements:
  - Ubuntu Linux (recommended version: 20.04 LTS or newer)
  - Docker Engine v20.10.x or newer
  - Docker Compose v2.x or newer
  - Git (for version control and downloading challenge materials)
  - Text editor or IDE of your choice (VSCode, Nano, Vim, etc.)
- Network requirements:
  - Ports 80, 81, and 443 must be open and available
  - Internet connection for downloading Docker images
  - Optional: Domain name(s) for configuring SSL certificates
  - Optional: Cloudflare account for DNS validation (if using Let's Encrypt)

## Installation

### 1. Install Docker Engine
```bash
# Update package index
sudo apt-get update

# Install prerequisites
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Add Docker repository
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Update package index again
sudo apt-get update

# Install Docker CE
sudo apt-get install -y docker-ce

# Add current user to docker group to run Docker without sudo
sudo usermod -aG docker $USER

# Apply group changes (alternatively, you can log out and log back in)
newgrp docker

# Verify Docker installation
docker --version
docker run hello-world
```

### 2. Install Docker Compose
```bash
# Install Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/v2.18.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# Apply executable permissions
sudo chmod +x /usr/local/bin/docker-compose

# Create symbolic link if needed
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

# Verify installation
docker-compose --version
```

### 3. Clone the Challenge Repository
```bash
# Clone the repository
git clone https://github.com/brandonleegit/homelabexplorers.git

# Navigate to the challenge directory
cd homelabexplorers/challenges/challenge1-dvincent
```

### 4. Create a Shared Docker Network
```bash
# Create a shared network for communication between containers
docker network create shared_network
```

## Configuration

### 1. Deploy Nginx Proxy Manager
```bash
# Navigate to the Nginx Proxy Manager directory
cd nginx-proxy-manager

# Start the containers
docker-compose up -d

# Verify containers are running
docker-compose ps
```

### 2. Deploy Sample Applications
```bash
# Navigate to the sample apps directory
cd ../sample-apps

# Start the containers
docker-compose up -d

# Verify containers are running
docker-compose ps
```

### 3. Access Nginx Proxy Manager
- Open a web browser and navigate to `http://your-server-ip:81`
- Log in with the default credentials:
  - Email: `admin@example.com`
  - Password: `changeme`
- You will be prompted to change the default credentials on first login

### 4. Configure Proxy Hosts
- In the Nginx Proxy Manager dashboard, go to "Proxy Hosts" and click "Add Proxy Host"
- For each application, configure:
  - Domain Name: Your chosen domain or subdomain
  - Scheme: http
  - Forward Hostname/IP: Name of the container (e.g., hello-world, wordpress, dashboard)
  - Forward Port: Internal port of the application (80 for hello-world and wordpress, 8000 for dashboard)
  - Enable SSL options if using domains with Let's Encrypt

## Verification

### 1. Test Application Access
- Access each application through its configured domain:
  - Hello World: `http://hello.yourdomain.com` (or the IP if not using domains)
  - WordPress: `http://wordpress.yourdomain.com`
  - Dashboard: `http://dashboard.yourdomain.com`

### 2. Verify SSL Configuration (if configured)
- Ensure all applications are accessible via HTTPS
- Verify SSL certificates are valid and properly installed
- Test HTTP to HTTPS redirection

### 3. Check Container Status
```bash
# Check the status of all running containers
docker ps

# View logs for Nginx Proxy Manager
docker-compose -f ~/nginx-proxy-manager/docker-compose.yml logs -f app

# View logs for sample applications
docker-compose -f ~/sample-apps/docker-compose.yml logs -f
```

## Troubleshooting

### Port Conflicts
- **Issue**: Cannot start Nginx Proxy Manager due to port conflicts
- **Solution**: Ensure ports 80, 81, and 443 are not in use by other services. Check with `sudo netstat -tulpn | grep -E '80|81|443'`

### Network Connectivity Issues
- **Issue**: Containers cannot communicate with each other
- **Solution**: Verify all containers are on the same network with `docker network inspect shared_network`

### SSL Certificate Problems
- **Issue**: Let's Encrypt certificates not being issued
- **Solution**: Ensure DNS records are properly configured and accessible from the internet

### Database Connection Errors
- **Issue**: Nginx Proxy Manager cannot connect to the database
- **Solution**: Check the MariaDB container is running with `docker ps`. If needed, restart with `docker-compose -f ~/nginx-proxy-manager/docker-compose.yml restart db`


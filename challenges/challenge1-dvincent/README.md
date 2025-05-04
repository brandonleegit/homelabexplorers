# Homelab Explorers: Challenge 1 - Level Up Your Stack

This repository contains the implementation of Challenge 1 from the Homelab Explorers project, focusing on deploying Nginx Proxy Manager as an ingress controller for Docker hosts, securing it with SSL via Let's Encrypt, and routing multiple applications through it by domain name.

## Project Structure

### `/docs`
Comprehensive documentation for the challenge:
- **overview.md**: Challenge objectives, skills developed, and prerequisites
- **setup.md**: System requirements and installation instructions
- **guide.md**: Step-by-step instructions with detailed explanations and diagrams
- **resources.md**: Links to relevant documentation, tutorials, and community resources

### `/nginx-proxy-manager`
Contains the Docker Compose configuration for Nginx Proxy Manager:
- **docker-compose.yml**: Defines the Nginx Proxy Manager and MariaDB containers
- **data/**: Stores Nginx Proxy Manager configuration data (generated at runtime)
- **letsencrypt/**: Contains SSL certificates from Let's Encrypt (generated at runtime)

### `/sample-apps`
Sample applications used to demonstrate proxy functionality:
- **docker-compose.yml**: Defines multiple sample applications (NGINX Hello, WordPress, Dashboard)
- **wordpress_data/**: WordPress application data volume (generated at runtime)
- **wordpress_db_data/**: WordPress database data volume (generated at runtime)

## Getting Started

1. Install Docker and Docker Compose as described in the setup.md file
2. Deploy Nginx Proxy Manager using the configuration in the nginx-proxy-manager directory
3. Deploy sample applications using the configuration in the sample-apps directory
4. Configure proxy hosts and SSL certificates as described in the guide.md file

## Network Architecture

The project uses a shared Docker network (`shared_network`) to enable communication between Nginx Proxy Manager and the sample applications. This allows Nginx Proxy Manager to route traffic to the appropriate containers based on domain names.

## SSL Certificates

The project demonstrates how to secure applications with Let's Encrypt SSL certificates using DNS validation through Cloudflare. The process is fully automated through Nginx Proxy Manager's integration with Let's Encrypt.

## Challenge Completion

This implementation successfully meets all the requirements of the challenge:
- ✅ Nginx Proxy Manager deployed as an ingress controller
- ✅ Applications secured with SSL via Let's Encrypt
- ✅ Multiple applications routed through the proxy by domain name

## Further Exploration

After completing this challenge, consider exploring:
- Advanced features of Nginx Proxy Manager (access lists, custom locations)
- Monitoring and logging for your proxy and applications
- Implementing container health checks and automatic restarts
- Creating a backup strategy for your configuration and certificates

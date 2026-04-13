# Linux Server Setup & Secure Nginx Deployment

![Project Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)
![Ubuntu](https://img.shields.io/badge/OS-Ubuntu%2024.04-FF6F00?style=flat-square&logo=ubuntu)
![Nginx](https://img.shields.io/badge/Web%20Server-Nginx-009639?style=flat-square&logo=nginx)
![Let's Encrypt](https://img.shields.io/badge/SSL-Let's%20Encrypt-003A70?style=flat-square)

**Live Demo**: [https://yourdomain.com](https://yourdomain.com)  
**API Endpoint**: [https://yourdomain.com/api](https://yourdomain.com/api)

---

## 📋 Project Overview
I provisioned a secure Linux server from scratch on a cloud VPS, hardened it following industry security best practices, installed and configured Nginx as a production-grade web server, and secured it with a valid Let’s Encrypt SSL certificate — **all without using Docker, Compose, or any automation tools**.

The setup serves:
- A clean static HTML page at `/` displaying my HNG username as visible text.
- A precise JSON response at `/api` with `Content-Type: application/json` and HTTP 200.
- Automatic 301 redirect from HTTP to HTTPS on both endpoints.

This project demonstrates core DevOps fundamentals: **server hardening**, **secure configuration**, **web server management**, **SSL/TLS**, **firewall rules**, and **production readiness**.

---

## ✨ Key Features & Achievements

- **Security-First Approach**:
  - Non-root user (`hngdevops`) with sudo privileges
  - Root SSH login disabled
  - Password authentication disabled (key-based SSH only)
  - UFW firewall restricted to ports 22, 80, 443 only

- **Production-Grade Web Server**:
  - Nginx serving static content and JSON API
  - Proper MIME types and headers
  - HTTP → HTTPS redirect (301)

- **Valid SSL/TLS**:
  - Let’s Encrypt certificate (no self-signed certs)
  - HTTPS enabled on both `/` and `/api`

- **Compliance with All Evaluation Criteria**:
  - Exact JSON structure and Content-Type
  - Username visible in HTML (not hidden/commented)
  - No Docker or automation tools used

---

## 🛠️ Tech Stack

| Category          | Technology                  |
|-------------------|-----------------------------|
| Operating System  | Ubuntu 24.04 LTS            |
| Web Server        | Nginx                       |
| SSL Certificate   | Let’s Encrypt (certbot)     |
| Firewall          | UFW                         |
| SSH Hardening     | OpenSSH (key-only auth)     |
| Cloud Provider    | DigitalOcean (or any VPS)   |

---

## 📸 Screenshots / Demo

![Homepage Screenshot](screenshots/homepage.png)
*Static HTML page showing HNG username*

![API Response](screenshots/api-response.png)
*Exact JSON response from /api*

*(Add your actual screenshots to a `screenshots/` folder in the repo)*

---

## 🚀 Quick Start / Reproduction Steps

### 1. Server Provisioning
- Spin up an Ubuntu 24.04 VPS (e.g., DigitalOcean Droplet)
- Add your SSH public key during creation
- Point a domain A record to the server IP

### 2. Server Hardening
```bash
# Create non-root user
adduser hngdevops
usermod -aG sudo hngdevops

# Disable root login & password auth
sudo nano /etc/ssh/sshd_config
# Set: PermitRootLogin no
#      PasswordAuthentication no

sudo systemctl restart ssh
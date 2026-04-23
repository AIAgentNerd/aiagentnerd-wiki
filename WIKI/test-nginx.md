---
title: Test Nginx
source_raw: test-nginx.md
compiled_at: 2026-04-23T15:43:06.033Z
type: system-note
tags: [aiagentnerd, system, wiki, compiled]
---

# Test Nginx

# Nginx Reverse Proxy with Cloudflare Tunnel and Port Configuration  

## Overview  
This document outlines the technical implementation of an Nginx reverse proxy integrated with a Cloudflare tunnel, including port configuration for secure and scalable deployment.  

---

## Prerequisites  
1. **Nginx Installed**: Ensure Nginx is installed and configured on the target server.  
2. **Cloudflare Account**: A Cloudflare account with access to the domain and tunnel management.  
3. **Domain Configuration**: The domain must be registered and DNS records properly configured.  

---

## Step-by-Step Setup  

### 1. Nginx Reverse Proxy Configuration  
Configure Nginx to act as a reverse proxy for the target service.  

**Example Configuration (`/etc/nginx/sites-available/default`)**  
```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```  
**Notes**:  
- Replace `example.com` with the target domain.  
- Adjust `proxy_pass` to match the upstream service port (e.g., `8080`).  
- Test configuration with `nginx -t` and reload with `systemctl reload nginx`.  

---

### 2. Cloudflare Tunnel Setup  
Use the Cloudflare tunnel to expose the Nginx service securely.  

**Install Cloudflare Tunnel**:  
```bash
curl -s https://packagecloud.io/install/repositories/cloudflare/cloudflared/script.deb.sh | sudo bash
sudo apt-get install cloudflared
```  

**Generate Tunnel Configuration**:  
Create a tunnel configuration file (`/etc/cloudflared/tunnel.yml`):  
```yaml
name: nginx-tunnel
url: http://localhost:80
credentials-file: /etc/cloudflared/tunnel.json
```  

**Start the Tunnel**:  
```bash
sudo cloudflared tunnel run nginx-tunnel
```  
**Notes**:  
- Replace `http://localhost:80` with the Nginx service endpoint.  
- Ensure the Cloudflare API token is stored securely in `tunnel.json`.  

---

### 3. Port Configuration  
**Nginx Port**:  
- Default: `80` (HTTP) or `443` (HTTPS).  
- Ensure the port is open on the server's firewall.  

**Cloudflare Tunnel Port**:  
- The tunnel automatically maps the Nginx port to a Cloudflare-assigned subdomain (e.g., `nginx-tunnel.example.com`).  
- Verify the tunnel status via the Cloudflare dashboard.  

---

## Validation  
1. Test Nginx proxy functionality by accessing the domain.  
2. Confirm Cloudflare tunnel is active and routing traffic correctly.  
3. Monitor logs for errors:  
   - Nginx: `tail -f /var/log/nginx/error.log`  
   - Cloudflare: `journalctl -u cloudflared`  

---

## Notes  
- **Security**: Use HTTPS with Let's Encrypt for production environments.  
- **Scalability**: Adjust Nginx worker processes and Cloudflare tunnel settings for high-traffic scenarios.  
- **Maintenance**: Regularly update Nginx and Cloudflare CLI to address vulnerabilities.  

---  
This note is intended for internal technical reference only. Do not share with external parties.

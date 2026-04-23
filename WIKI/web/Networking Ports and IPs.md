---
title: Networking Ports And IPs
source_raw: web/Networking Ports and IPs.md
compiled_at: 2026-04-23T15:34:02.105Z
type: system-note
tags: [aiagentnerd, system, wiki, compiled]
---

# Networking Ports And IPs

# Networking Ports and IPs

## Overview

This document provides an in-depth understanding of networking ports and IP addresses, specifically tailored to the AiAgentNerd system architecture. It explains the significance of IPs and ports in routing network traffic, the role of Cloudflare Tunnel, and the importance of port management for system security and functionality.

## IP Address

An IP address identifies a device on a network. There are two types of IP addresses:

### Local IP (Private IP)

Used inside a network (home/server LAN). Examples include `127.0.0.1` (localhost) and `192.168.x.x` or `10.x.x.x`. In the AiAgentNerd system, `http://127.0.0.1:3100` refers to the local machine on port 3100.

### Public IP

Used to reach a server from the internet. However, in the AiAgentNerd system, public IPs are not used directly due to the implementation of Cloudflare Tunnel.

## Port

A port is like a door to a specific service. Each app runs on a different port. In the AiAgentNerd system, ports are used as follows:

- Hermes: 3100 (Backend brain)
- Static UI (python): 8080 (Frontend)
- Hermes dashboard: 9119 (Web UI)
- NGINX: 80/443 (Public web traffic)

## Listening on a Port

When an app runs, it listens on a specific port for incoming requests. For example, running `node server.js` starts the server and listens on port 3100.

## Request Flow

When a user opens `https://x.aiagentnerd.com`, the request flow is as follows:

1. Browser → Cloudflare
2. Cloudflare → Tunnel
3. Tunnel → Server
4. NGINX (or direct route)
5. Routed to a port: 3100 → API, 8080 → UI, 9119 → dashboard

## Importance of Ports

Ports are critical for the following reasons:

1. Avoid conflicts: Only one app can use a port at a time.
2. Separate responsibilities: Different services are kept on different ports.
3. Security: Ports can be blocked or exposed selectively.

## Localhost vs 0.0.0.0

- `127.0.0.1` (localhost): Accessible only from the same machine.
- `0.0.0.0`: Accessible from anywhere on the network.

In the AiAgentNerd system, Hermes is reachable from the local machine, LAN, and via tunnel due to running on `http://0.0.0.0:3100`.

## NGINX Role

NGINX acts as a receptionist, listening on ports 80 (HTTP) and 443 (HTTPS), and forwarding traffic internally. This is known as reverse proxy.

## Cloudflare Tunnel

Cloudflare replaces the need for public IPs and port forwarding. It routes traffic through a tunnel to the local machine on a specific port, ensuring the server's IP and ports are never exposed directly.

## System Architecture

The simplified architecture of the AiAgentNerd system is as follows:

```
User Browser
     ↓
Cloudflare (DNS + HTTPS + Access)
     ↓
Cloudflare Tunnel
     ↓
Your Server
     ↓
NGINX (optional)
     ↓
Port routing:
   → 8080 (UI)
   → 3100 (Hermes API)
   → 9119 (dashboard)
```

## Importance for AiAgentNerd

Understanding ports is foundational for the AiAgentNerd system. It enables routing agents, exposing services, and debugging issues. With this understanding, one can add new agents, route subdomains, separate UI/backend/workers, and scale the system effectively.

## Summary

- **IP = which machine**
- **Port = which app on that machine**

This document is a technical guide for the AiAgentNerd system repository, focusing on the internal workings of networking ports and IPs.
